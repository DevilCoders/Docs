# VictoriaMetrics в Вертикалях

## Координаты
**Морда (promxy)**:
  - прод: [https://prometheus.vertis.yandex.net](https://prometheus.vertis.yandex.net)
  - тестинг: [https://prometheus-testing.vertis.yandex.net](https://prometheus-testing.vertis.yandex.net)

**Внутренний балансировщик для запросов PromQL (адреса для grafana datasource):**
  - прод: http://vmselect-agg-api.vrts-slb.prod.vertis.yandex.net/select/0/prometheus
  - тестинг: http://vmselect-agg-api.vrts-slb.prod.vertis.yandex.net/select/1/prometheus

**Графики:**
  [VM](https://grafana.vertis.yandex-team.ru/d/Ds1pxd4Mk/vm)

**Список и состояние алертов (promxy):**

  - прод: [https://prometheus.vertis.yandex.net/alerts](https://prometheus.vertis.yandex.net/alerts)
  - тестинг: [https://prometheus-testing.vertis.yandex.net/alerts](https://prometheus-testing.vertis.yandex.net/alerts)

**Список, состояние и статистика скрейп-эндпоинтов (из vmagent):**
  - прод: [https://prometheus.vertis.yandex.net/targets](https://prometheus.vertis.yandex.net/targets)
  - тестинг: [https://prometheus-testing.vertis.yandex.net/targets](https://prometheus-testing.vertis.yandex.net/targets)

**Состояние (доступность) шардов vmstorage:**
  [https://prometheus.vertis.yandex.net/vmstorage](https://prometheus.vertis.yandex.net/vmstorage)

**Репозиторий с конфигурацией, правилами алертов и recording rules:**
  [prometheus-config](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config)

**Адреса для приёма метрик через пуш-модель (pushgateway):**
  - прод: [http://prometheus-pushgateway-prod-int.slb.vertis.yandex.net/](http://prometheus-pushgateway-prod-int.slb.vertis.yandex.net/)
  - тестинг: [http://prometheus-pushgateway-test-int.slb.vertis.yandex.net/](http://prometheus-pushgateway-test-int.slb.vertis.yandex.net/)


## Общие сведения
Используем кластерную версию стека VictoriaMetrics.
[https://victoriametrics.com/](https://victoriametrics.com/)
[https://docs.victoriametrics.com/Cluster-VictoriaMetrics.html](https://docs.victoriametrics.com/Cluster-VictoriaMetrics.html)

Стек компонентов являет собой отказоустойчивую и горизонтально масштабируемую альтернативу Prometheus, с совместимым API на запись и чтение: приложения экспортируют метрики в привычном prometheus-формате (есть реализации экспорта метрик и библиотеки под многие языки программирования; многие приложения имеют поддержку экспорта именно в этом формате); кроме того, чтение из VM так же осуществляется в совместимом с prometheus API, имеется полная поддержка языка запросов PromQL. Это обеспечивает возможность использовать Grafana так, как будто мы работаем с обычным prometheus.
Кроме того, есть ряд дополнительных плюшек, вроде возможности приёма метрик в форматах Graphite, Influx; расширение над языком запросов PromQL - [MetricsQL](https://docs.victoriametrics.com/MetricsQL.html); и др.

Типичная архитектура кластера описана в [документации проекта](https://docs.victoriametrics.com/Cluster-VictoriaMetrics.html#architecture-overview). В упрощённом виде наш стек выглядит так:

![vm-simple](vm-simple.png)
В наших реалиях, в связи с тем, что требуется отказоустойчивость в условиях жизни в нескольких ДЦ, с бесшовным переключением, схема несколько сложнее.

[Более развёрнутая схема](https://jing.yandex-team.ru/files/wf1nder/vm-full-1.png)

## Тестинг, тенанты
Метрики из тестингового окружения отделены от метрик из прод-окружения. Тем не менее, бОльшая часть компонентов стека - общие для тест и прод данных, за некоторыми исключениями. Физически данные разных окружений хранятся в общих стораджах, для разделения используем механизм [Multitenancy](https://docs.victoriametrics.com/Cluster-VictoriaMetrics.html#multitenancy). Для прода используется тенант ```0```, для тестинга - ```1```.
Лишь малая часть компонентов стека имеет отдельные экземпляры под конкретное окружение, а именно:

  - [vmagent](#vmagent)
  - [rr-executer](#rr-executer)
  - [prometheus-pushgateway](#prometheus-pushgateway)

## Репликация
Полноценной репликации у VM в общепринятом понимании нет. Данные пишутся и хранятся в нескольких ДЦ, при этом вся цепочка по сбору, хранению и транспорту метрик выполняется для каждого ДЦ параллельно. В случае временной недоступности части компонентов или всего стека в каком-то ДЦ, например во время учений, в данном ДЦ образуется гэп - отсутствие данных за период недоступности. Это компенсируется наличием данных по метрикам за этот период на стораджах в соседних ДЦ. Финальное "склеивание" метрик/графиков происходит автоматически и бесшовно так, что клиенты/пользователи никак не зааффекчены и не замечают гэпов.

Компоненты кластера VM развёрнуты в следующих ДЦ:
  - sas
  - vla


## Компоненты
Каждый компонент стека так или иначе задублирован внутри и/или между ДЦ, поэтому выход из строя по любой причине части инстансов или компонента целиком не приводит к деградации сервиса в целом.

### vmagent
В нашей инсталляции используется для получения экспортируемых метрик с эндпоинтов (приложений) и последующей отправки их далее, в компонент vminsert, попутно применяя правила [relabeling](https://docs.victoriametrics.com/#relabeling)'а.
Отправка производится в стандартном для prometheus формате `remote write`.
Мы используем service-discovery через consul для автоматического сбора метрик с приложений, для чего задействован отдельный кластер consul agent'ов (см. [vm-consul-agent](#vm-consul-agent)). Кроме sd, есть так же статическая конфигурация эндпоинтов.
Синтаксис конфигов соответствует таковому у prometheus, используется только секция ```scrape_configs```.

Конфигурация vmagent приезжает из репозитория: [https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config)
(см. файлы `production/scrape.yml`  и `testing/scrape.yml`). Для редактирования конфигурации нужно сделать соответствующий pull request, после выполнения тестов появится возможность смержить изменения в мастер, что стриггерит выкладку конфигов.
Выкладка изменеий состоит из нескольких этапов:

  - результирующие наборы правил выгружаются в S3 [джобой](https://t.vertis.yandex-team.ru/buildConfiguration/VertisAdmin_PrometheusValidateConfigs_UploadArc?mode=builds)
  - раз в 5 минут соответствующие джобы в rundeck ([прод](https://rundeck.vertis.yandex.net/project/sandbox/job/show/1b46d1e4-6a49-417b-847b-d82806055ee1), [тестинг](https://rundeck.vertis.yandex.net/project/sandbox/job/show/8ef4b1e8-f40c-40d1-be9d-fcc5d8ab3d46)) инициируют скачивание конфига из S3 непосредственно на хостах с vmagent скриптом ```vmagent-mkconfig.sh``` ([прод](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/vmagent/files/production/vmagent-mkconfig.sh), [тестинг](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/vmagent/files/testing/vmagent-mkconfig.sh)), который сравнивает конфиг с локальным, и в случае, если есть расхождения, применяет новую конфигурацию.

Смотреть полный список эндпоинтов, с которых vmagent скрейпит данные (включая те, что обнаружены через service discovery), статус и некоторую статистику по каждому эндпоинту можно на странице ```/targets``` на морде кластера (см. [Координаты](#koordinaty)). Данная страница генерируется vmagent'ом, в который с морды проброшена вышеуказанная ручка.

По одному инстансу vmagent запущено в ДЦ sas и vla, которые полностью идентичны друг другу: скрейпят одни и те же данные с одних и тех же источников, и затем пушат их в одни и те же приёмники [vminsert](#vminsert). Таким образом обеспечивается отказоустойчивость: при падении одного инстанса поставка метрик не прерывается. Так же это означает, что в приёмники приходят дублированные данные, и в каждом временном ряду получается в 2 раза больше точек. Это не вызывает проблем, лишь несколько повышенную нагрузку на запись и бОльшее потребление дискового пространства. В VM есть [механизмы дедупликации](https://docs.victoriametrics.com/#deduplication), сводящие на нет данные недостатки, однако мы их пока не используем.

**Где живёт:**
Один из немногих компонентов стека, поселённый отдельно в тестинговом и продовом окружении. Связано это с тем, что нужны доступы для скрейпа метрик с приложений/эндпоинтов в соответствующих окружениях.
Прод: lxc, группа `%vertis_vprod_vmagent`
Тестинг: lxc, группа `%vertis_vtest_vmagent`
Наливка:
  [https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_vprod_vmagent.yml](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_vprod_vmagent.yml)
  [https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_vtest_vmagent.yml](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_vtest_vmagent.yml)
  [https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/vmagent](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/vmagent)
Каркас пакета: общий пакет
  [victoria-metrics](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/victoria-metrics)
Сборка: общая сборка
  [victoria-metrics](https://t.vertis.yandex-team.ru/project/VertisAdmin_VictoriaMetrics?mode=builds)

### vminsert
Первый из трёх основных компонентов в кластерном стеке VictoriaMetrics.
Принимает данные в формате `remote write`  (в нашем случае от [vmagent](#vmagent)), и отправляет их далее в инстансы компонента [vmstorage](#vmstorage). Отправка происходит с учётом hashring, и в каждый шард vmstorage отправляются данные только по метрикам, которым положено жить на этом шарде. Таким образом обеспечивается более-менее равномерное распределение нагрузки и данных по шардам.
Выбор шарда для каждой метрики условен: во время недоступности шарда данные по метрикам, которые должны были записываться на него, отправляются на другие шарды. Таким образом, при недоступности шарда данные не теряются, распределяясь по другим шардам в кластере.
Сам же hasрring генерируется на основе текущего списка шардов, который передаётся в vminsert в виде списка в аргументах командной строки. Таким образом, при изменении списка шардов hashring изменяется, и происходит перераспределение записи данных по метрикам по шардам. Логически это не вызывает проблем, т.к. при чтении поиск по метрикам производится параллельно по всем шардам, однако перешардирование означает мгновенное создание большого количества новых тайм-серий на каждом шарде, что создаёт высокую нагрузку на него, и может временно сделать шард недоступным. В таких ситуациях рекомендуется закрывать с него чтение через [vmclose](#zakrytie-sharda-vmstorage-ot-nagruzki).
В VM есть механизм "[репликации](https://docs.victoriametrics.com/Cluster-VictoriaMetrics.html#replication-and-data-safety)" (название спорное), когда данные по каждой метрике записываются более, чем на 1 шард, например на свой + следующий шард, обеспечивая хранение по схеме N+1 для повышения надёжности. Однако мы это пока не используем, т.к. у нас данные и так дублируются между ДЦ: в каждом ДЦ свой полный набор данных по всем метрикам, распределённый по шардам.
vminsert - полностью stateless-компонент, который отлично живёт в облаках и масштабируется обычным увеличением количества инстансов.

**Где живёт:**
shiva/nomad, сервисы:
  - [vminsert-sas](https://a.yandex-team.ru/arc_vcs/classifieds/services/deploy/vminsert-sas.yml)
  - [vminsert-vla](https://a.yandex-team.ru/arc_vcs/classifieds/services/deploy/vminsert-vla.yml)

Исходники контейнера: общий контейнер
  [victoria-metrics](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-dockerfiles/victoria-metrics)
Сборка: общая сборка
  [victoria-metrics](https://t.vertis.yandex-team.ru/project/VertisAdmin_VictoriaMetrics?mode=builds)

### vmstorage
Второй основной компонент в стеке. Обеспечивает непосредственно хранение данных по метрикам на дисках. vmstorage живёт на физических серверах с большими HDD-дисками. Каждый инстанс являет собой шард, на котором хранится какая-то плюс-минус равная часть от общего объёма данных по метрикам в ДЦ.
К настоящему времени пришли к схеме, когда на одном физическом сервере размещён один шард-инстанс: в 1 ДЦ имеем 3 шарда, всего 3 физических сервера.
vmstorage взаимодействует с компонентами [vminsert](#vminsert), который пушит в него данные по метрикам в соответствии с hashring, и с [vmselect](#vmselect), который производит вычитывание данных по запросам от пользователей/клиентов.

**Где живёт:**
Железные серверы, группы `%vertis_prod_victoria`
Наливка:
  [https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_prod_victoria.yml](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_prod_victoria.yml)
  [https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/victoria](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/victoria)

Каркас пакета: общий пакет
  [victoria-metrics](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/victoria-metrics)
Сборка: общая сборка
  [victoria-metrics](https://t.vertis.yandex-team.ru/project/VertisAdmin_VictoriaMetrics?mode=builds)

### vmselect
Третий основной компонент стека VM. Выполняет поиск по метрикам и отдачу данных по ним, выполняет запросы в формате PromQL. Является прослойкой между читающим клиентом (условной графаной) и стораджем VM ([vmstorage](#vmstorage)).
На каждый входящий запрос vmselect выполняет поиск данных по метрикам параллельно на всех нодах [vmstorage](#vmstorage), перечисленных в его конфигурации (аргументах запуска). Чаще всего отдельная метрика расположена на одном конкретном шарде в каждом ДЦ. Однако она так же может оказаться более чем на одном шарде одновременно - если включить режим "[репликации](https://docs.victoriametrics.com/Cluster-VictoriaMetrics.html#replication-and-data-safety)", при котором данные пишутся на N+1 шард, либо читаем сразу из нескольких ДЦ. Так же метрика с течением времени может "переезжать" между шардами. Во всех этих случаях vmselect корректно "склеивает" все результаты поиска от всех шардов [vmstorage](#vmstorage), и выдаёт обобщённый ответ на запрос.

**Где живёт:**
shiva/nomad, сервис:
  [vmselect-agg](https://a.yandex-team.ru/arc_vcs/classifieds/services/deploy/vmselect-agg.yml)
Исходники контейнера: общий контейнер
  [victoria-metrics](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-dockerfiles/victoria-metrics)
Сборка: общая сборка
  [victoria-metrics](https://t.vertis.yandex-team.ru/project/VertisAdmin_VictoriaMetrics?mode=builds)

#### Балансировка над vmstorage, "склеивание" результатов поиска
Нам интересно использовать один общий кластер vmselect, чтобы обращаться сразу ко всем шардам во всех ДЦ, обеспечивая тем самым отказоустойчивость: уметь отвечать на запросы, если данные по метрикам есть хотя бы в одном ДЦ; в то же время, в обычном рабочем режиме данные присутствуют сразу в трёх ДЦ. Однако в документации к VM рекомендуется использовать по отдельному кластеру vmselect в каждом локальном ДЦ, чтобы ходить в шарды [vmstorage](#vmstorage) только внутри ДЦ, и не ходить из vmselect в [vmstorage](#vmstorage) кросс-ДЦ. Частично это связано с тем, что vmselect плохо умеет в connection-timeout, и, видимо, это [сложно починить](https://github.com/VictoriaMetrics/VictoriaMetrics/issues/711). Нас это аффектит тем, что vmselect на каждый входящий запрос отправляет запросы и ждёт ответа от каждого шарда прежде, чем сам ответит на запрос. Если один или несколько шардов становятся недоступны (ушли на учения, либо проблемы с железным хостом), то все запросы начинают тормозить или совсем таймаутиться - ждём полный таймаут, отведённый на выполнение запроса, не понимая, что некоторые шарды просто недоступны.
Ранее мы использовали схему с отдельными vmselect в каждом ДЦ, а над ними, перед графаной, у нас был [promxy](https://github.com/jacksontj/promxy). В целом, с задачей он справлялся, проблем с заданием conn timeout не имел. Однако имел некоторые другие проблемы и спецэффекты, разнящиеся от версии к версии. В итоге [была изобретена схема](https://st.yandex-team.ru/VERTISADMIN-25938), всё же позволяющая использовать один общий vmselect над всеми [vmstorage](#vmstorage), и, таким образом, отзакаться от promxy в качестве "балансера" над несколькими [vmselect](#vmselect). Помог нам в этом [haproxy](http://www.haproxy.org/). Суть в том, чтобы заимплементить недостающий в vmselect connection timeout при обращении к шардам vmstorage.
Суть реализации: в [контейнер с vmselect](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-dockerfiles/victoria-metrics) был добавлен haproxy. В контейнер мы передаём список всех шардов vmstorage, и при старте выполняется скрипт, который итерируется по списку шардов, формируя конфиг для haproxy таким образом, чтобы для каждого шарда создавалась отдельная секция. Каждая секция - фактически балансировщик с единственным апстримом (шардом vmstorage), на отдельном порту. Ключевые опции чека, позволяющие разрывать соединение от vmselect при недоступности апстрима:
```check on-marked-down shutdown-sessions inter 1s```
Далее запускается vmselect, в который передаются аргументы ```-storageNode=``` со всеми адресами и портами локального haproxy.
Таким образом, haproxy выступает в качестве прокси 1=1 между vmselect и vmstorage, выполняя проверки живости vmstorage, и отправляя на входящие от vmselect запросы reject в случае, если чек не прошёл в течение 1 секунды, что говорит о недоступности соответствующего шарда. vmselect же корректно обрабатывает такую ситуацию, исключая соответствующий шард из обработки, и не ожидая от него ответа. При этом учитываются ответы от всех доступных шардов. Таким образом обработка запросов продолжает работать в штатном режиме, без задержек и каких бы то ни было проблем до тех пор, пока доступны все шарды хотя бы из одного ДЦ.
![vm-vmselect-agg](vm-vmselect-agg.png)

На haproxy так же включена статусная страница, отображающая состояние всех апстримов (шардов vmstorage). Страница прокинута в морду в ручку /vmstorage, см. [Координаты](#koordinaty).

### vm-consul-agent
Поскольку [vmagent](#vmagent) в процессе выполнения service discovery создаёт значительную нагрузку на consul-agent, производительности локально установленного на хостах consul agent'а оказывается недостаточно, что приводит к сбоям обновления конфигурации, и к зажиганию мониторинга consul agent'а на хосте. Для решения этой проблемы было решено сделать отдельный кластер consul agent'ов в облаке, состоящий из нескольких инстансов в ДЦ, специально выделенный для использования с [vmagent](#vmagent)'ом.

**Где живёт:**
shiva/nomad, сервис:
  [vm-consul-agent](https://a.yandex-team.ru/arc_vcs/classifieds/services/deploy/vm-consul-agent.yml)
Исходники контейнера:
  [vm-consul-agent](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-dockerfiles/vm-consul-agent)
Сборка:
  [vm-consul-agent](https://t.vertis.yandex-team.ru/project/VertisAdmin_VmConsulAgent?mode=builds)

### rr-executer
Вспомогательный компонент, написанный в Вертикалях, используемый для выполнения [recording rules](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/).
Ранее выполнением занимался [promxy](https://github.com/jacksontj/promxy), однако в какой-то момент его производительности для выполнения всех правил перестало хватать, и было решено написать собственный компонент с учётом именно наших особенностей эксплуатации. К примеру, каждое правило из каждой группы (yaml-файла) выполняется параллельно остальным, в отдельной go-рутине. Таким образом, выполнение одного тяжёлого правила не влияет и не приостанавливает выполнение других правил.
Ещё одна особенность: результат выполнения не отправляется в VM через протокол ```remote write```, как это делают другие аналогичные сервисы, а вместо этого экспортируются в виде обычных prometheus-метрик, которые впоследствии скрейпит [vmagent](#vmagent). Плюс подхода - нет проблем с отправкой большого количества данных по результирующим метрикам, не нужно тюнить и подбирать настройки remote write. Минус - результат выполнения оказывается в VM с небольшим запозданием: scrape interval (10 секунд) + 5-10 секунд на внутренние перекладывания внутри rr-executer, итого 20-30 секунд.
Правила recording rules хранятся в [репозитории](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config), см. директории ```production/recording-rules``` и ```testing/recording-rules```.

Для прод- и тестинг-окружения выполняются отдельные инстансы rr-executer.
Кроме того, сервис так же разделён на отдельные сервисы по ДЦ: sas и vla. Сделано это по той причине, что запускать более 1 инстанса сервиса в ДЦ не стоит, т.к. rr-executer оказывает ощутимую нагрузку на vmselect и vmstorage. В то же время, текущие средства деплоя (shiva/nomad) не позволяют корректно работать с сервисами, имеющими по одному инстансу в ДЦ, и при этом более 1 ДЦ присутствия: если у такого сервиса запустить деплой или рестарт, будет произведён параллельный перезапуск инстансов сервиса во всех ДЦ. Поскольку у сервиса всего по одному инстансу в ДЦ, это приведёт к тому, что в какой-то момент, в течение (пере)запуска не будет выполняться ни один инстанс rr-executer. Что, в свою очередь, ведёт к появлению пропусков на всех графиках.

**Где живёт:**
jenkins/nomad, сервисы:
  - прод:
    - [rr-executer-sas](https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/production/job/rr-executer-sas/)
    - [rr-executer-vla](https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/production/job/rr-executer-vla/)
  - тестинг:
    - [rr-executer-sas](https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/testing/job/rr-executer-sas/)
    - [rr-executer-vla](https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/testing/job/rr-executer-vla/)

Исходники сервиса, контейнера:
  [rr-executer](https://a.yandex-team.ru/arc_vcs/classifieds/infra/rr-executer)

Сборка:
  [rr-executer](https://t.vertis.yandex-team.ru/project/VertisAdmin_RrExecuter?mode=builds)

### prometheus-juggler
Вспомогательный компонент, написанный в Вертикалях, используемый для трансляции событий от alert rules (получаемых сейчас от promxy, а в последствии, возможно, от vmalert) в собятия для Juggler.
Сами alert rules хранятся в [репозитории](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config), см. директории ```production/alerts``` и ```testing/alerts```.
Для прод- и тестинг-окружения выполняются отдельные инстансы prometheus-juggler, однако оба они в прод окружении, т.к. читают из [vmselect](#vmselect), который так же выполняется только в прод-окружении.

**Где живёт:**
jenkins/nomad, сервисы:
  - прод:
    - [prometheus-juggler](https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/production/job/prometheus-juggler/)
  - тестинг:
    - [prometheus-juggler-testing](https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/production/job/prometheus-juggler-testing/)

Исходники:
  [prometheus-juggler](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-juggler)
Cобирать через `ya make`.

### Juggler-generate
Скрипт, генерирующий и выливающий в Juggler алерты из prometheus-алертов. Выполняется в Teamcity, триггерится на изменения в [prometheus-алертах](#alerty-i-recording-rules).

Скрипт: [juggler-generate.py](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config/utils/juggler-generate.py)
Джоба в Teamcity: [Juggler generate](https://t.vertis.yandex-team.ru/buildConfiguration/VertisAdmin_PrometheusValidateConfigs_JugglerGenerate?mode=builds)

### prometheus-pushgateway
Компонент, позволяющий принимать метрики в push-модели вместо стандартной для prometheus pull-модели. Не рекомендуется к использованию, т.к. не обеспечивает отказоустойчивости: выполняется всегда только в 1 экземпляре в силу особенностей его реализации.
Планируем [попробовать отказаться от pushgateway в пользу vmagent](https://st.yandex-team.ru/VERTISADMIN-26690), чтобы решить проблему отсутствия отказоустойчивости.

Адреса для приёма метрик: см. [Координаты](#koordinaty)

**Где живёт:**
jenkins/nomad, сервисы:

  - прод: [prometheus-pushgateway](https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/production/job/prometheus-pushgateway/)
  - тестинг: [prometheus-pushgateway](https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/testing/job/prometheus-pushgateway/)

Исходник контейнера:
  [prometheus-pushgateway](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-dockerfiles/prometheus-pushgateway)
Сборка:
  [prometheus-pushgateway](https://t.vertis.yandex-team.ru/project/VertisAdmin_PrometheusPushgateway?mode=builds)

### promxy
Сторонний компонент, не входящий в стек VM.
Мы уже отказались от promxy в качестве [исполнителя recording rules](#rr-executer), однако всё ещё используем его для двух вещей: выполнение [alert rules](#alerty-i-recording-rules), а так же в качестве веб-морды, в которой можно исполнять отдельные запросы PromQL. Тем не менее, мы не теряем надежды однажды закопать promxy совсем. В этом случае для выполнения алертов предполагается перейти на [vmalert](https://docs.victoriametrics.com/vmalert.html) (который так же, возможно, заменит и [rr-executer](#rr-executer)). Веб-морда, возможно, будет разобрана совсем за ненадобностью (одиночные запросы можно и удобно выполнять в [grafana explore](https://grafana.com/docs/grafana/latest/explore/)), либо будет заменена на что-то другое.
promxy поселен отдельно под прод- и тестинг-метрик, однако в обоих случаях он выполняется в прод-окружении. Связано это с тем, что читает из [vmselect](#vmselect), который так же живёт только в прод-окружении.

**Где живёт:**
jenkins/nomad, сервисы:
  - прод: [promxy-vm](https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/production/job/promxy-vm/)
  - тестинг: [promxy-vm-testing](https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/production/job/promxy-vm-testing/)

Исходники контейнера:
  [promxy-vm](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-dockerfiles/promxy-vm)
Сборка:
  [promxy-vm](https://t.vertis.yandex-team.ru/project/VertisAdmin_PromxyVm?mode=builds)

## Алерты и recording rules
Оригинальный Prometheus имеет механизмы выполнения alerting rules - заранее описанные правила алертов, срабатывающих при переходе пороговых значений по метрикам; а так же recording rules - фонового выполнения заранее описанных запросов, результат выполнения которых записывается в виде новых метрик. Немного документации:

  [Alreting rules](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/)
  [Recording rules](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/)

Оба вида правил имеют схожую структуру, описанную в виде yaml-файлов, и активно используются у нас в Вертикалях.
На момент резвёртывания инсталляции VictoriaMetrics, нативного компонента для выполнения таких правил в стеке не было, поэтому были задействованы альтернативные компоненты, используемые и по сей день:

  - алерты исполняются через [promxy](#promxy), затем статус чеков транслируется в [Juggler](https://wiki.yandex-team.ru/sm/juggler/) через [prometheus-juggler](#prometheus-juggler)
  - recording rules выполняются через компонент [rr-executer](#rr-executer), результат выполения в виде новых метрик пишется (экспортируется) компонентом обратно в VM

Есть надежда, что со временем оба компонента будут разобраны и заменены на соответствующий компонент из стека VictoriaMetrics, появившийся относительно недавно - [vmalert](https://docs.victoriametrics.com/vmalert.html).

Оба вида правил живут в репозитории [https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config), в соответствующих директориях:

  - алерты:
    - прод: [prometheus-config/production/alerts](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config/production/alerts)
    - тестинг: [prometheus-config/testing/alerts](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config/testing/alerts)
  - recording rules:
    - прод: [prometheus-config/production/recording-rules](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config/production/recording-rules)
    - тестинг: [prometheus-config/testing/recording-rules](https://a.yandex-team.ru/arc_vcs/classifieds/infra/prometheus-config/testing/recording-rules)

Для того, чтобы добавить/удалить/отредактировать правило, нужно сделать соответствующий pull-request в репозиторий. По завершении выполнения [тестов](https://t.vertis.yandex-team.ru/buildConfiguration/VertisAdmin_PrometheusValidateConfigs_ValidateArc?mode=builds), появится возможность смержить изменения в мастер, что стриггерит выкладку изменений.
Выкладка изменеий состоит из нескольких этапов:
  - результирующие наборы правил выгружаются в S3 [джобой](https://t.vertis.yandex-team.ru/buildConfiguration/VertisAdmin_PrometheusValidateConfigs_UploadArc?mode=builds)
  - из S3 изменения подхватываются соответствующим компонентом:
    - promxy: раз в 60 секунд [скрипт](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-dockerfiles/promxy-vm/mkconfig.sh) внутри контейнера скачивает, распаковывает и сравнивает набор правил с тем, что у него уже есть локально. Если есть различия, то имеющийся в контейнере набор замещается новым, и promxy заново применяет все правила
    - rr-executer: раз в 30 секунд [скрипт](https://a.yandex-team.ru/arc_vcs/classifieds/infra/rr-executer/mkconfig.sh) внутри контейнера скачивает, распаковывает и сравнивает набор правил с тем, что у него уже есть. Если есть различия, то имеющийся в контейнере набор замещается новым, и rr-executer заново применяет все правила

Смотреть список и состояние алертов можно на странице ```/alerts``` на веб-морде кластера, см. [Координаты](#koordinaty).

Альтернативно [заводить алерты можно и в графане](https://grafana.com/docs/grafana/latest/alerting/).

## Использование токенов-секретов в scrape-конфигурации
В запросах для скрейпа метрик из Яндекс Облака необходимо использовать аутентификацию через токен, который, в свою очередь, нужно безопасно хранить. Для решения этой задачи в скрипт формирования конфига для vmagent добавили логику, которая вытаскивает секреты из секретницы, и подставляет в нужные места в результирующем конфиге.

### Как добавить секрет
Для добавления нового токена его нужно положить в виде нового ключа (фактически выпустить новую версию секрета с добавлением ключа) в соответствующий секрет:

[Тестинг](https://yav.yandex-team.ru/secret/sec-01fzanhx0xbv5hw2f0kmssdgy7/explore/versions)
[Прод](https://yav.yandex-team.ru/secret/sec-01fzap1tggvy27jnsmhjsrh23b/explore/versions)

В качестве имени ключа удобно использовать `folderId` облака, однако можно использовать и произвольное имя.
В самом конфиге секрет указывать через шаблон:
```
${TOKEN:<key_name>}
```

[Пример](https://a.yandex-team.ru/arcadia/classifieds/infra/prometheus-config/testing/scrape.yml?rev=r9395057#L665):
```
    bearer_token: '${TOKEN:b1gv58n8k4k9qof9shir}'
```

## Траблшутинг
### Закрытие шарда vmstorage от нагрузки
В случае, если один или несколько шардов создают проблемы для работы VM (тормоза, таймауты при чтении), стоит "закрыть" этот шард от нагрузки. Выявить такой шард можно, как правило, по высокому LA (выше 50 на хостах во vla, выше 30 на хостах в остальных ДЦ). Подобное изредка случается на выходе из учений, когда на вновь вернувшихся шардах в один момент создаётся большое количество новых тайм-серий.
Для закрытия написан скрипт [vmclose.sh](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/victoria/files/usr/bin/vmclose.sh), раскатанный на хосты с шардами [vmstorage](#vmstorage).

```
# vmclose.sh

Usage:
vmclose.sh close         close vmstorages from vmselect
vmclose.sh open          open vmstorages from vmselect
vmclose.sh show          show vmstorage's closed ports
```

При "закрытии" в iptables создаётся правило с REJECT на соответствующий tcp-порт. Такое состояние порта корректно обрабатывается на haproxy и прокидывается в [vmselect](#vmselect), приводя к тому, что шард перестаёт использоваться при запросах на поиск метрик.
В общем случае, закрытие одного или всех шардов в ДЦ, или даже всех шардов в двух ДЦ, не должно привести к деградации сервиса, поскольку полный набор данных по метрикам есть в каждом ДЦ, и, соответственно, для корректной работы должен быть доступен полный набор шардов хотя бы в одном ДЦ.

Состояние (доступность) шардов vmstorage можно смотреть на соответствующей статусной странице, см. [Координаты](#koordinaty).
