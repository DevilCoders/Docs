## Квоты DNS запросов рекурсивных контуров
На DNS контурах рекурсивных ресолверов могут быть установлены квоты на количество запросов для каждого проекта в Компании. Необходимость таких квот была осознана в рамках серии тикетов [[3](https://st.yandex-team.ru/TRAFFIC-13116)] и инцидентов [[4](https://st.yandex-team.ru/LSR-683)], [[5](https://st.yandex-team.ru/SPI-26214)], общий смысл которых сводился к проблемам при отстутствии изоляции потребителей, а именно, - неконтроллируемый рост нагрузки на рекрусивный dns одного проекта вызывал отказ в обслуживании dns инстансов и аффектил остальных. Примерами таких генераторов нагрузок были проекты, в которых массовый ресолвинг внешних dns является частью их бизнес логики: ``zora``, ``antispam``, и т.п. Деятельность подобных проектов сводится к необходимости ресолвинга имён в набор ``ip`` адресов и тем самым проверки валидности имён. В инфраструктуре также есть проекты, которые в силу своей организации могут периодически генерировать исключительно внутренний dns трафик, отличающийся от наблюдаемого бейзлайна на несколько порядков [[1](https://st.yandex-team.ru/TRAFFIC-13246/)], [[2](https://st.yandex-team.ru/TRAFFIC-13259)] Такой рост нагрузки идентифицируется как неконтролируемый со стороны источника и требует изоляции. Для единого распределяемого dns ресолвинга такой изоляцией может быть квотирование dns запросов на стороне контуров. 

Мотивация:
* **``[1]``** [TRAFFIC-13246](https://st.yandex-team.ru/TRAFFIC-13246/) - повышенный rate dns-cache pid 10bba57 **500Krps** SAS600Krps VLA SAAS_STABLE_BASE_NETS
* **``[2]``** [TRAFFIC-13246](https://st.yandex-team.ru/TRAFFIC-13259/) - повышенный rate **700Krps** VLA на dns pid 0x522 CMSEARCHNETS
* **``[3]``** [TRAFFIC-13116](https://st.yandex-team.ru/TRAFFIC-13116/) - квотирование dns запросов на dnsguard кеширующих ресолверов
* **``[4]``** [LSR-683](https://st.yandex-team.ru/LSR-683/) - проблемы с DNS: ns-cache и dns-cache перестали справляться с нагрузкой
* **``[5]``** [SPI-26214](https://st.yandex-team.ru/SPI-26214) - ZORA: Сломалась часть DNS (ALL)

Под локациями мы понимаем:
* **``локации``**: ``IVA``, ``MYT``, ``MAN``, ``SAS``, ``VLA``

Под контурами рекурсивных ресолверов: 
* **``эникаст``** ``dns`` сервисы: ``ns+cache``, ``dns+cache``
* **``локационные``** ``dns`` сервисы: ``ns+cache-sas``, ``ns+cache-vla``, ``ns+cache-man``, нагрузка на которые подаётся из ``rtc`` ``dns manager`` как на основной ``endpoint`` для dns ресолвинга, с возможностью переключения нагрузки на ``эникаст`` контур в случае отказа ``локационного``

Под dns ресолвингом:
* **``внутренним``** - называем нативный ресолвинг (без использования ответов кеша) для осуществления которого не требуется обращения к авторитетам зон, находящихся вне сетей Яндекса. В частности, считаем что весь ресолвинг зон, авторитетами которых являются dns серверы Яндекса ``ns1+ns2``, ``ns3+ns4``, **``ns5+ns6``**, а также чисто внутренние авторитеты ``YP`` -- внутренний. Для рекурсивных контуров также предполагаем что используется ``root zone`` файл, предоставляющий текущее состояние зона, авторитетами которых являеются ``root`` ``dns``. При таком использовании цепочка обхода авторитетов для всех наших зон может быть выполнена локально инстансом dns сервера -- без обращения по сети 
* **``внешним``** - называем процесс ресолвинга, который использует внешние по отношению к Яндексу авторитеты. 

Под dns квотами (рекурсивных контуров) и лимитами (на источник):
* **``квоты``** - это количество ``pps`` для ``dns`` запросов источников, идентифицированных ``dnsguard`` принадлежаших к одному ``projectid``. Значение ``projectid`` парсится из ``src ip`` запроса, либо из ``edns subnet client`` расширения при его наличии. Такую опцию добавляет для запросов из ``rtc`` ``dns manager``[[7](https://st.yandex-team.ru/RTCNETWORK-406)]. Квоты могут быть установлены для ``projectid`` на контур, на локацию, и, в крайнем случае на конкретный инстанс. Целевая картина распределения квот между проектами формируется на уровне контуров с учётом групп локаций: 1-ая группа [``SAS``, ``VLA``], 2-ая группа: [ ``IVA``, ``MYT``, ``MAN``]. Выбор групп обусловлен характером перетекающего трафика между локациями и взаимная возможность по терминированию траффика одной локации на контурах другой (см. схему дублирования dns эникастовых и локационных контуров). Установлены следующие правила квотирования:
  *  потребители менее чем **``50pps``** на ноду на радары системы квотирования не попадают, для них специальные квоты не выставлены, лимиты не вычисляются, мониторинг и алертинг выключёны. Как только генерация трафика становится выше этого значения то проект опадает на ``default`` квоты, значения которых заданы для всех незаданных явно конфигурацией значений ``projectid`` (см. пункт квотирование потребителей, [[8](https://a.yandex-team.ru/arcadia/noc/traffic/dns/junk/d2/QUOTAS.md#kvotirovanie-potrebitelej)])
  * процесс назначения и вычисления квот начинается с ``dry-run`` режима системы, в которой по квотам формируются лимиты, однако, фактического ``rate limit`` на ``dnsguard`` не устанавливается. Процесс обучения модели квот требуется для оценки актуальных квот. После стабилизации мониторинга система переводится в рабочий режим: ``dry-run`` снимается и на ``dnsguard`` приезжают фактические значения ``rate limit`` и он готов к блокировке превышающего квоты траффика. **Сейчас мы находится в режиме запуска ``dry-run`` режима для всех контуров и локаций** по тикету [TRAFFIC-13116](https://st.yandex-team.ru/TRAFFIC-13116/). 
  * квоты, выставленные для инстанса ``dns`` (что по конфигурационному дереву ниже квот на локацию) при вычислении лимитов вычитаются из пула распределяемых между инстансами локационных квот. Это правило действует для каждого конфигурируемого ``projectid``, то есть некоторая квота на инстансе может быть фисированной для выбранного ``projectid``, а остальные распределяются как квоты из пула инстансов на локацию)

* **``лимиты``** - это количество ``pps`` уровней [``black``, ``red``, ``yellow``, ``green``] для ``projectid`` установленных на **``каждом``** инстансе dns контуров цель которых: **(a)** обеспечение схемы блокирования dns трафика выше допустимо заданного (уровня ``black``) через возможности ``dnsguard``, **(b)** мониторинг текущего потребления квоты источниками ``projectid`` разного уровня критичности -- от ``red`` до ``green``. Фактически ``лимиты`` -- это реализация заданных ``квот`` для каждого ``dns`` инстанса соответствующих контуров и локаций в условиях (1) различных весов инстансов (2) различного количества доступных инстансов. В том числе, опционально, сценарий по выпадению половины мощностей локации должен приводить к переспределению `лимитов`` при тех же квотах, (см. пункт квотирование потребителей, [[8](https://a.yandex-team.ru/arcadia/noc/traffic/dns/junk/d2/QUOTAS.md#kvotirovanie-potrebitelej)])
 
Под dnsguard:
 * **``dnsguard``** - ``xdp`` программа подсчитывающая статистику для ``projectid`` и ограничивающая входной ``rate`` ``dns`` запросов установленным в её конфигурации значением, а также демон по управлению конфигурацией и получению статистики [[6](https://st.yandex-team.ru/TRAFFIC-10478)]. При превышении ``rate`` ``limit`` очередной ``dns`` запрос дропается, со стороны клиента это выглядит как потеря пакета и ``timeout`` на ожидание ответа. Тут нужно понимать, что в большом количестве случаев это вызывает дополнительные повторы отправки клиентом запросов и мультипликацию общего рейта в сторону ``dns`` контуров.

Под графиками ``dns`` квот:
* **``графики dns для projectid``** - <span style="color:red">**T.B.D.**</span>

Под мониторингом ``dns`` квот:
 * **``мониторинг dns квот``** - **для ответственных со стороны ``dns``** - это набор следующих алертов и их аггрегатов (в терминологии ``juggler`` и их мульти-алертов (в терминологии ``solomon``) для каждого сущности ``projectid`` которого есть на радарах системы квотирования, см расшифровку аггрегатов ниже в [[8](https://a.yandex-team.ru/arcadia/noc/traffic/dns/junk/d2/QUOTAS.md#monitoring-potrebitelej)] Полный список сооветствующих juggler проверок может быть найден по тегу [tag=dns-quotas](https://juggler.yandex-team.ru/aggregate_checks/?project=dns&query=tag%3Ddns-quotas) в самом ``juggler``, сейчас это такой список:
    * **juggler**: [dns-quotas-byabc](https://juggler.yandex-team.ru/project/dns/aggregate?host=dns-core-quotas&service=dns-quotas-byabc&project=dns) - аггрегаты ``rawevents`` проверок для каждого ``abc`` проекта. Для ``abc`` проекта может быть целый список ``projectid`` попадающих в него, проверка аггрегирует этот список и выдаёт обобщённый результат 
    * **juggler**: [dns-quotas-bypid](https://juggler.yandex-team.ru/project/dns/aggregate?host=dns-core-quotas&service=dns-quotas-bypid&project=dns) - аггрегаты ``rawevents`` для каждого ``projectid``
    * **juggler**: [dns-quotas-bylocation](https://juggler.yandex-team.ru/project/dns/aggregate?host=dns-core-quotas&service=dns-quotas-bypid&project=dns) - аггрегаты ``rawevents`` для каждого ``location``, в него включаются списки по сервисам и по ``projectid`` таким образом что алерты аггрегируются по ``pps`` уровням мониторинга - в порядке ``black``, ``red``, ``yellow``, ``green``
    * **juggler**: [dns-quotas-byhost](https://juggler.yandex-team.ru/project/dns/aggregate?host=dns-core-quotas&service=dns-quotas-byphost&project=dns) - специальный низко-уровневый аггрегат для диагностики поведения лимитов, формирует общий алерт на состояние хоста целиком, для всех ``projectid`` которые там есть. Нужно понимать что алерты выше уровня могут триггерится, при этом состояние самого хоста быть ок.
    * **solomon**:  <span style="color:red">**T.B.D.**</span>

* **``service alerting``** - **для ответственных со стороны проектов** - <span style="color:red">**T.B.D.**</span>

### Система квотирования и мониторинга dns запросов рекурсивных контуров
Общая схема системы квотирования включает в себя следующие последовательно действующие компоненты: 

* **cбор метрик** - каждый ``dns`` инстанс отправляет в сторону ``dns`` аггрегаторов метрик текущую статистику ``dnsguard`` для ``projectid`` со скоростью досаточной для реакции на стороне мониторинга и алертинга в течении 1 минуты после появления дегрдации (превышения лимитов). Обычно каждый инстанс шлёт такие данные каждые ``5`` секунд в сторону **всех** мастеров ``dns-core`` аггрегации, выбранных для этого этапа (см детали ниже в [[9](https://a.yandex-team.ru/arcadia/noc/traffic/dns/junk/d2/QUOTAS.md?edit=true&preview=true#kvotirovanie-potrebitelej)])

* **аггрегация метрик** - для всех полученных метрик каждый мастер делает следующее **(a)** валидирует полученные значения, (см. ``EstimateMetric`` метод в [[A](https://a.yandex-team.ru/arcadia/noc/traffic/dns/junk/d2/core/dnsguard.go)], временно до починки ``dnsguard`` со вздрыжнями из [TRAFFIC-13242](https://st.yandex-team.ru/TRAFFIC-13242)), **(б)** сопоставляет ``projectid`` и ``abc`` проекта для каждой метрики **(в)** аггрегирует значения для каждого ``dns`` контура и локации **(г)** вычисляет в какой класс мониторинга относятся полученые метрики относительно лимитов, заданных для каждого ``projectid`` **(д)** формирует и отправляет ``pps`` и расширенные для алертинга метрики (см. тикет <span style="color:red">**T.B.D.**</span>) в ``solomon`` проект ``dns-metrics`` [[Б](https://solomon.yandex-team.ru/?project=tt&cluster=dns-metrics&service=dns-metrics&sensor=aggregate-pass-pps)]. В дальнейшем ``multi-alert`` формирует статус по мониторингу квот. Этот процесс называется **``cooker``**, он работает каждые ``10`` секунд.

* **квотирование потребителей** - на вход этой детали поступает **(a)** текущая конфигурация квот, **(б)** текущее состояние инстансов, их распределение по сервисам и локациям, их веса **(в)** наличие метрик от инстанса. Процесс под названием **``quoter``** вычисляет по входным данным фактические лимиты, которые нужно отдать в ``dnsguard`` для ``rate limit`` (если система работает не в режиме ``dry-run``) и мониторинг и алертинг. Он работает над перевычислением всех лимитов каждые ``10`` секунд.

* **мониторинг потребителей** - по аггрегированным метрикам, для которых уже вычислены значения мониторинга, формируются ``rawevents`` сгруппированные по списку ``dns-quotas-byabc``, ``dns-quotas-bypid``, ``dns-quotas-bylocation``, ``dns-quotas-byhost``. Это требует переформирования метрик в группы и вычисления сосответствующих групповых статусов. При этом уже являясь аггегаторами в указанном смысле, это метрики ``rawevents`` поставляются в ``juggler`` и для них, в свою очередь, существуют ещё аггрегаторы более высокого уровня. Для ``juggler`` аггрегатов устанавливается ``NODATA_CRIT`` - так как ``projectid`` могут исчезать из мониторинга (когда dns траффик отствутвует из источников этого проекта). Для ``solomon`` требуются расширенные метрики (см. тикет <span style="color:red">**T.B.D.**</span>)

* **обучение модели квот** - процесс итерационного подбора значений квот и их уровней мониторинга для ``projectid``, осуществляющийся в течении статистически значимого времени (например, ``7`` дней), при котором происходит увеличение текущих значений проектов до актуальных (см. тикет <span style="color:red">**T.B.D.**</span>)

* **конфигурирование контуров** - каждая нода ``dns`` контуров, участвующая в квотировании, ждёт для себя конфигурации ``лимитов``. Вычисленные процессом ``quoter`` лимиты распределяются в конфигурациях и применяются на инстасах ``dns``. Так вычисленные лимиты для ``dnsguard`` на мастер нодах ``dns-core`` появляются в конфигурации ``dnsguard`` через процесс ``d2``. Все конфигурации и квот и лимитов хранятся и управляются в ``zookeeper`` кластере. Как только соответствующая конфигурации ``dns`` инстанса обновится или будет создана установленные ``watches`` сигнализируют о том что нужно внести изменение в ``dnsguard`` (или любую другую подсистему). В режиме ``dry-run`` изменения в ``dnsguard`` не выкатываются а остаются только на уровне мониторинга и алертинга.

#### Сбор метрик
Сборк метрик осуществляет ``d2`` запущенный на нодах ``dns`` инстансов. Сам ``d2`` знает метрики каких контуров нужно собирать. Конфигурация процесса управления на нодах выглядит так:
```yaml
dnsguard:
  # device to monitor if xdp installed
  dev: "eth0"

  # url to get data or put some restrictions
  api: "http://[::1]:8080/api/v1"

  # collector settings to push dnsguard
  # metrics to masters, configuration is
  # used for client and master sides
  collector:

     # collector is enabled and one time
     # per counter below pushes dnsguard
     # metrics to master aggregator, http
     # side, also see storage part
     enabled: true

     # metrics are gathered each interval of
     # seconds per minutes, e.g. 1, 5, 10, 12
     intervals: 12

     # after d2 starts it need some time to 
     # gather statistics and push only correct
     # data of interval later these seconds
     startup-waittime: 30

     # minimal pps for pass+drop to be
     # collected, e.g. it could be 10 or 
     # 20, 200 per second, also used in
     # estimate correctness algorithm
     minimal: 50

     # master endpoints (resolved via map) 
     master:
        # tcp port data in collector master    
        port: 6651

        # collector pushes to 6651/tcp data
        nodes:
         - "dns-core01f.berry.yandex.net"
         - "dns-core01v.berry.yandex.net"
         - "dns-core01s.berry.yandex.net"
         - "alpha-30v.lxd.tt.yandex.net"

```

Основные параметры: **``master``** - набор мастер нод, куда нужно отправлять метрики, обычно нода отправляет на все мастера которые есть в системе. Отправка в мастер не означает что метрики пройдут полный путь обработки и поступят на вход в мониторинг и алертинг - для этого есть отдельная конфигурация соответствующих подсистем ``cooker``, ``quoter``. Опция **``minimal``** определяем минимальный ``pps`` для ``projectid``, который в итоге попадаёт на радары. 

Метод отправки можно вызывать из командой строки ``dns`` ноды соответствующего класса, (это ``ns+cache``, ``rtc+dnscache``) следующим образом:
```sh
    # запускаем на ноде "ns02e.name.yandex.net", указываем класс
    # метрики "dnsguard", хотим увидеть debug

    d2 metrics collect --class="dnsguard" --debug

    DEBU[2022/07/30 - 16:40:29.827] [576532]:[1] (collect) (metrics) request to collect dnsguard metrics 
    DEBU[2022/07/30 - 16:40:29.827] [576532]:[1] iva location:'ns02e.name.yandex.net', node:'(collect) (metrics)' 
    DEBU[2022/07/30 - 16:40:29.853] [576532]:[1] (collect) (metrics) [0] pid:'0x640' counters pass:'250716471.00' drop:'0.00', pps pass:'230.88' drop:'0.00' 
    DEBU[2022/07/30 - 16:40:29.853] [576532]:[1] (collect) (metrics) [1] pid:'0x522' counters pass:'103386815.00' drop:'0.00', pps pass:'51.68' drop:'0.00' 
    ...
    DEBU[2022/07/30 - 16:40:29.868] [576532]:[116] [01]/[01] {"success":true,"messages":[{"code":202,"message":"Accepted"}] } 
    DEBU[2022/07/30 - 16:40:29.868] [576532]:[1] (metrics) finished in '41.570267ms' 
    DEBU[2022/07/30 - 16:40:29.868] [576532]:[1] d2 metrics collecting finished over classes:['dnsguard'] 
```
#### Аггрегация метрик
Получение и первичную аггрегацию метрик осуществляет ``d2`` запущенный на мастер нодах кластера ``dns-core``. Для того чтобы развести процессы приёма и батчевой обработки запросов используется локально поднятый на каждой ноде ``redis``. Его цель - организовать очередь обработки метрик, в которую через ``api`` метод ``dns`` инстансы складируют свои метрики, а просыпающийся раз в ``10`` секунд процесс ``cooker`` вычитывает их (см. ``RPOPLPUSH``), формирует задания для обогащения метрик ``abc`` ``abcid``.

Для ресолвинга соотношения ``projectid`` используется нетривиальная механика через **2** поддерживаемых асинхронно маппинга: ``(1)``:  ``projectid`` ->  ``[]string{servicerole}``,``(2)``: ``servicerole`` -> ``abc, abcid``. Эти два маппинга потребляются из ``rt`` и ``abc`` соответственно предоставляя в памяти быстрый доступ к этим соответствиям. Однако, есть нюансы:
* в некоторых случаях для первого соответствия в ресолвинге оказываются несколько ``servicerole``, и соответственно, может оказать что для одного ``projectid`` есть целый список ``abc`` проектов. В этом случае, берётся какой-то первый, не факт что правильный. Тут можно будет вернуться и сделать как правильно, фактически нужно вести список ``abc`` проектов и дублировать весь алертинг в этот список
* бывает так что в первом соответствии нету ни одной ``servicerole``, а есть например, группа по стафф, в этом случе результат маппинга устанавлвиается в ``default`` ``abc`` проект ``dostavkatraffica``

Далее процесс сверки значений ``pps`` выполняется для каждого ``projectid`` как для хостов так и аггрегировано для локаций. Аггрегаты для локаций строятся по полученным метрикам и соотнесения метрик хостов к локациям и сервисам. Каждая метрика проходит процесс валидации значений чтобы избежать вздрыжней. Для этого ``d2`` ведёт некоторую историю метрики ``pps counters`` и может сделать оценку полученного ``pps``, если полученное значение больше чем оценка, такая метрика выкидывается. Такие некорректные метрики могут возникать из-за особенности подчёта в ``dnsguard``, а также на стыках рестартов процессов (возможно).

Одним из входом процесса является маппинг ``лимитов``. В случае если в маппинге есть для сервиса, для локации для ``projectid`` значения лимитов они и используются для вычисления алерта. Если в маппинге не обнаруживается соответствие алгоритм использует ``default`` конфигурацию, такого вида
```yaml
  # used for client and master sides
  collector:
     # master endpoints (resolved via map) 
     master:
        # cooker manages a process to aggregate
        # metrics, enrich them, calculating quotes
        # and push dns-metris into solomon (see
        # solomon section
        cooker:
           # beware to process all metrics received                
           enabled: true
           # cooker should have a list of limits for
           # each projectid defined from quoter, see
           # quoter section, for project ids that
           # is not defined in a list we have a default
           # limits per host and per location
           limits:

              # if not enabled some predefined limits
              # used for quotes, see below
              enabled: true

              # some fallback values for monitoring
              # stage of cooking, if < 0 no actually
              # comparision is done and classes
              # always "green", a quad is 
              fallback-host-pps: [-1, -1, -1, -1]
              fallback-location-pps: [-1, -1, -1, -1]

              # if no any projectid defined we have
              # some defaults pps per host and location
              default-host-pps: [4000, 2750, 2500, 1250]
              default-location-pps: [10000, 7500, 5000, 1000]
```

Если маппинг существует (его формирует процесс ``quoter``) то он выглядит так, для примера локации ``iva`` и набора ``projectid`` ``0x121``, ``0xf803``:
```json
{
   "uuid": "b8dbcd7a-5957-479d-b2c7-ff2e2e68fa1f",
   "type": "config+limits",
   "created": "2022-07-30T17:12:16.070060878+03:00",
   "updated": "2022-07-30T17:12:16.070060878+03:00",
   "path": "/dns-core/config/s/l/h/t/limits",
   "limits": {
      "location": {
         "iva": {
            "0x121": [
               100,
               75,
               50,
               25
            ],
            ...
            "0xf803": [
               15999.999999999998,
               12000,
               7500,
               4999.999999999999
            ]
         },
         ...
      }
   }
```

В итоге процесс ``cooker`` формирует набор метрик, которые он отгружает в два места: **(a)** solomon для графиков и алертинга и в **(b)** блок мониторинг потребителей в виде ``juggler`` ``rawevents``. Обогащенные и проверянные метрики выглядят так:
```json

   {
      "id": "pass-pps",
      "value": 75.23877832230892,
      "tags": {
         "abc": "dostavkatraffika",
         "abcid": "1192",
         "class": "green",
         "dns-service": "ns-cache",
         "fqdn": "ns04f.name.yandex.net",
         "location": "myt",
         "projectid": "0xbacef6ff",
         "quota": "4000.0000",
         "weight": "1"
      },
      "Timestamp": 1659190697
   },
...   
   {
      "id": "aggregate-pass-pps",
      "value": 8744.081850490285,
      "tags": {
         "abc": "cloud-platform",
         "abcid": "3304",
         "class": "yellow",
         "dns-service": "ns-cache",
         "location": "myt",
         "projectid": "0xf803",
         "quota": "16000.0000",
         "weight": "1"
      },
      "Timestamp": 1659190762
   },
...  
```

Расширенные метрики в ``solomon`` - <span style="color:red">**T.B.D.**</span>

Существует команда для одного последовательного запуска итерации ``cooker``
```sh
    # запускаем на одном dns-core мастере, например, на alpha
    # ноде alpha-30v.lxd.tt.yandex.net 

    d2 metrics cook --debug --dry-run --class="dnsguard"

    DEBU[2022/07/30 - 17:23:33.570] [451930]:[1] (cook) (metrics) request to cook dnsguard metrics 
    DEBU[2022/07/30 - 17:23:33.570] [451930]:[1] vla location:'alpha-30v.lxd.tt.yandex.net', node:'(cook) (metrics)' 
    ...
    DEBU[2022/07/30 - 17:23:33.749] [451930]:[1] (metrics) (events) batches:[64]/[1] (of '29') 
    DEBU[2022/07/30 - 17:23:33.749] (statistics) [01]/[07] {                     
    DEBU[2022/07/30 - 17:23:33.749] (statistics) [02]/[07]    "timestamp": 1659191013, 
    DEBU[2022/07/30 - 17:23:33.749] (statistics) [03]/[07]    "time": "2022-07-30 17:23:33.74939274 +0300 MSK m=+0.195774564", 
    DEBU[2022/07/30 - 17:23:33.749] (statistics) [04]/[07]    "seconds-processed": 0.016596503, 
    DEBU[2022/07/30 - 17:23:33.749] (statistics) [05]/[07]    "input-metrics": 376, 
    DEBU[2022/07/30 - 17:23:33.749] (statistics) [06]/[07]    "output-metrics": 29 
    DEBU[2022/07/30 - 17:23:33.749] (statistics) [07]/[07] }                     
```   
#### Квотирование потребителей
Под квотированием потребителей понимается процесс вычисления ``лимитов`` для мониторинга, алертинга и конфиуграции ``dnsguard`` для каждого инстанса ``dns`` контуров из существующих установленных в системе ``квот``. Для этого на вход процесс ``quoter`` поступает конфигурация ``квот``, инстансов сервисов и история метрик. Последнее для определения нужно ли распределять квоту на этот инстанс -- если система его распознает как ``alive`` то квоты локации на него распределятся.

Процесс строит дерево распредление квот, заданных в системе. Квоты могут быть устанолвены на один из следующих объектов системы квотирования: сервис, сервис+локация, сервис+локация+хост. Так как соотношение между ``сервис`` -> ``локация`` один-многим как и ``локация`` -> ``хост``, то в обобщённом виде конфигурация квот задаётся в виде дерева. При этом в каждом узле дерева есть классификация по ``projectid``. Всё это означает что для каждого ``projectid`` дерево может быть различным и для каждого ``projectid`` дерево может обходится по-разному, в зависимости от того есть ли в узле дереве конкретное значение ``projectid`` или нет.

Дерево ``квот`` выведенное как таблица имеет вид (в частном случае чтобы показать несколько различных типов конфигураций):
```sh
+--------------------------------------------------------------------+------------------------------------------------------+---------------------+---------+
|                                PATH                                |                        QUOTAS                        |       UPDATED       |   AGE   |
+--------------------------------------------------------------------+------------------------------------------------------+---------------------+---------+
| /dns-core/config/s/ns+cache/l/h/t/quotas                           | 0xdeadbeef:'[1000.0000]'                             | 2022-07-29 17:38:08 | 24.45h  |
|                                                                    | 0xf803:'[16000.0000 12000.0000 7500.0000 5000.0000]' |                     |         |
|                                                                    | 0x85632:'[1103.0000 825.0000 550.0000 275.0000]'     |                     |         |
+--------------------------------------------------------------------+------------------------------------------------------+---------------------+---------+
| /dns-core/config/s/ns+cache/l/iva/h/ns06e.name.yandex.net/t/quotas | 0x121:'[100.0000 75.0000 50.0000 25.0000]'           | 2022-07-26 11:11:57 | 102.89h |
|                                                                    | 0x85612:'[100.0000 75.0000 50.0000 25.0000]'         |                     |         |
|                                                                    | 0xdeadbeef:'[1000.0000]'                             |                     |         |
+--------------------------------------------------------------------+------------------------------------------------------+---------------------+---------+
| /dns-core/config/s/l/h/t/quotas                                    | 0x85612:'[1000.0000 750.0000 500.0000 250.0000]'     | 2022-07-25 11:00:17 | 127.08h |
|                                                                    | 0x85632:'[1100.0000 825.0000 550.0000 275.0000]'     |                     |         |
|                                                                    | 0xdeadbeef:'[1001.0000]'                             |                     |         |
+--------------------------------------------------------------------+------------------------------------------------------+---------------------+---------+
```

Конфигурация процесса ``quoter`` выглядит так
```yaml
  # collector settings to push dnsguard
  # metrics to masters, configuration is
  # used for client and master sides
  collector:
     # master endpoints (resolved via map) 
     master:
        # configuration for dnsguard and for
        # monitoring data limits (used by cooker)
        # it could watch a list of quotes configurations
        # or perioidically recalculate limits
        # w.r.t quotes
        quoter:
           # process should be started as a periodical
           # recalculations and as a watches
           enabled: true

           # cooker statistics json file
           statistics-file: "/var/tmp/d2-quoter.json"

           # quoter as a result of its work generates
           # a list of limits per host for dnsguard, we could 
           # define here as a last resort whitelist
           # to update dnsguard configurations, if whitelist
           # is empty - quoter updates ALL hosts
           whitelist: [ "alpha-05v.lxd.tt.yandex.net" ]

           # sleep interval: quoter should process quotes
           # to limits and sleep for these seconds before
           # next try, could be 120, 60, 10
           sleep-interval: 10

           # quoter processors - a list of nodes that calculates
           # limits from quotes and generates limits dnsguard
           # updates configs (create and update), see also
           # send-processors below
           quoter-processors: [ "dns-core01f.berry.yandex.net", "alpha-30v.lxd.tt.yandex.net" ]

           # quoter could detect an age of metric
           # received and could skip nodes without
           # metrics in keepalive data of metrics
           # of less than indicated below expired
           # limit
           metrics:

             # skipping expired nodes     
             expired: false

             # a number of seconds for host metrics
             # to be detected as alive instance
             alive: 300

           # quoter uses a list of services and
           # location to manage, converting quotes
           # to limits and rate limits for
           # each host
           services:
             "ns+cache": [ "alpha", "iva", "myt" ]
             "rtc+dnscache": []

```

Процесс ``quoter`` запускается раз в ``sleep-interval`` секунд и только на процессорах из указанных в списке ``quoter-processors``. Это означает что не каждый мастер занимается реализацией доведения квот до лимитов для каждой локации и инстансов в ней. Важный параметр ``whitelist`` определяет работает ли вся схема квотирования в режиме ``dry-run`` или лимиты доводятся до конфигурации ``dnsguard``. Указанные в этом парметры ноды принимают изменения в ``rate limit`` и работают в боевом режиме.

Выходом этого процесса являются: **(a)** рассчитанные лимиты, примеры этого маппинга мы видели раньше в аггрегации метрик, **(b)** если система работает в боевом режиме то применение лимитов в конфигурациях ``dns`` инстансов. Для единократного запуска ``quoter`` есть команда ``d2`` выполняемая на одном из мастеров
```sh
    # запускаем рассчёт квот процессом quoter на ноде
    # alpha30v.lxd.tt.yandex.net в режиме dry-run: то есть
    # сформированные лимиты не будут установлены в системе

    d2 config quotas calc --debug --dry-run

    DEBU[2022/07/30 - 18:15:05.437] [518742]:[1] (config) (quotas) (calc) request to calc limits and quotas 
    DEBU[2022/07/30 - 18:15:05.437] [518742]:[1] (quota) (calc) (limits) tree lising over root:'/dns-core/config' 
    ...
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [01]/[17] { 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [02]/[17]    "uuid": "895008af-8111-4421-98f0-584d9dd14281", 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [03]/[17]    "type": "config+dnsguard", 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [04]/[17]    "owner": "dns", 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [05]/[17]    "created": "2022-07-29T17:38:09.883478762+03:00", 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [06]/[17]    "updated": "2022-07-29T17:38:09.883704169+03:00", 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [07]/[17]    "path": "/dns-core/config/s/ns+cache/l/vla/h/alpha-05v.lxd.tt.yandex.net/t/dnsguard", 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [08]/[17]    "pps_limits": { 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [09]/[17]       "any_project_id": -1, 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [10]/[17]       "per_project_id": { 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [11]/[17]          "0x85612": 1000, 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [12]/[17]          "0x85632": 1103, 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [13]/[17]          "0xdeadbeef": 1000, 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [14]/[17]          "0xf803": 16000 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [15]/[17]       } 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [16]/[17]    } 
    DEBU[2022/07/30 - 18:15:06.027] [518742]:[1] (dnsguard) (limits) (calc) [17]/[17] } 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) fqdn:'alpha-05v.lxd.tt.yandex.net' action:'ACTION+UPDATE' 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [01]/[17] { 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [02]/[17]    "uuid": "4d35590c-b0c6-4d25-aff7-24353442610b", 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [03]/[17]    "type": "config+dnsguard", 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [04]/[17]    "owner": "dns", 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [05]/[17]    "created": "2022-07-30T18:15:06.028039177+03:00", 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [06]/[17]    "updated": "2022-07-30T18:15:06.028039177+03:00", 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [07]/[17]    "path": "/dns-core/config/s/ns+cache/l/vla/h/alpha-05v.lxd.tt.yandex.net/t/dnsguard", 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [08]/[17]    "pps_limits": { 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [09]/[17]       "any_project_id": -1, 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [10]/[17]       "per_project_id": { 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [11]/[17]          "0x85612": 1000, 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [12]/[17]          "0x85632": 1103, 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [13]/[17]          "0xdeadbeef": 1000, 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [14]/[17]          "0xf803": 16000 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [15]/[17]       } 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [16]/[17]    } 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) [17]/[17] } 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (dnsguard) (limits) (calc) configs detected as EQUAL 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (quota) (calc) (limits) finished in '590.380754ms' 
    DEBU[2022/07/30 - 18:15:06.028] [518742]:[1] (limits) (calculating) finished in '590.406958ms' 
```   
#### Мониторинг потребителей
Формирование ``rawevents`` для ``juggler`` занимается процесс ``cooker`` как последний этап своей работы. Для ``solomon`` он же высылает неаггрегированные но протеггированные значениями в надежде что их можно использовать будет для ``multi alerts``. На текущий момент пересобираем это место в тикете (см. тикет <span style="color:red">**T.B.D.**</span>). Конфигурация для ``rawevents`` процесс ``cooker`` выглядит так
```yaml
        # solomon section
        cooker:
              # a max number of items in raw events
              # description (they sorted w.r.t pps)
              description-items-max: 8

              # if we should send data as raw events
              # into juggler
              rawevents-processors: [ "dns-core01f.berry.yandex.net", "alpha-30v.lxd.tt.yandex.net" ]

              # each raw events has some prefix to
              # classify data pushed suffix is 
              # derived from rawevents-enabled
              rawevents-prefix: "dns-quotas"

              # possible rawevents types to send
              rawevents-enabled: [ "events+byhost", "events+bypid", "events+bylocation", "events+byabc" ]

              # rawevents could have some tags calculated
              # by events processor and some statics
              rawevents-tags: [ "dns", "dns-quotas" ]

              # juggler expects that not more than 100
              # events are sent by one time, so we need
              # batching, possible values e.g. 32, 64, 72
              rawevents-batch: 64
```

В процессе вычисления ``rawevents``, которые в свою очередь также являются аггрегатами используются следующие форматы значений:
* ``dns-quotas-events-byabc`` - аггрегаторы по ``abc`` 
```json
      {
         "host": "alpha-30v.lxd.tt.yandex.net",
         "service": "dns-quotas-events-byabc-taxistorages3mds",
         "status": "OK",
         "description": "e:'EVENTS+BYABC' id:'taxistorages3mds' as service:'ns-cache' [0/0/0/48] GREEN (48) ['HOST: PASS: ns06e:73.7005:'0x41af',
                          ns03e:70.3202:'0x41af',ns02e:70.0805:'0x41af',ns04e:69.9830:'0x41af',ns05e:67.9560:'0x41af',ns04f:67.5912:'0x41af',
                          ns03f:64.8677:'0x41af',ns05f:63.3909:'0x41af'...,LOCATION: PASS: myt:374.0252:'0x41af',iva:360.5860:'0x41af'']
                          :'OK' 'OK'",
         "tags": [
            "dns",
            "dns-quotas",
            "dns-quotas-events-byabc"
         ]
      }

```
* ``dns-quotas-events-bypid`` - аггрегаторы по ``projectid`` 
```json
      {
         "host": "alpha-30v.lxd.tt.yandex.net",
         "service": "dns-quotas-events-bypid-0x41af",
         "status": "OK",
         "description": "e:'EVENTS+BYPID' id:'0x41af' as service:'ns-cache' [0/0/0/48] GREEN (48) ['HOST: PASS: ns06e:73.7005,ns03e:70.3202,
                         ns02e:70.0805,ns04e:69.9830,ns05e:67.9560,ns04f:67.5912,ns03f:64.8677,ns05f:63.3909...,LOCATION: PASS: myt:374.0252,
                         iva:360.5860'] :'OK' 'OK'",
         "tags": [
            "dns",
            "dns-quotas",
            "dns-quotas-events-bypid"
         ]
      },
```

Далее эти ``rawevents`` ещё раз аггрегируются но уже в ``juggler``, см. список аггрегаторов ``juggler`` [tag=dns-quotas](https://juggler.yandex-team.ru/aggregate_checks/?project=dns&query=tag%3Ddns-quotas)

#### Обучение модели квот
Изначально непонятно какие квоты ставить на какие ``projectid``. Решением этой задачи занимается процесс **``learner``**. Он начинает работать с любого распределения квот, в течении статистически продолжительного времени подстраивает значений квот всех уровеней (во основном увеличивает их так чтобы текущее распределение было ниже ``green`` уровня). Процесс ``learner`` ориентируется на некоторую группировку локаций так чтобы учитывать перераспределение трафика между локациями и возможную терминацию на разных контурах. В том числе взаимозаменяемость ``ns+cache``, ``rtc+dnscache``, (см. тикет <span style="color:red">**T.B.D.**</span>).

#### Конфигурирование контуров
Для того чтобы рассчётные значени лимитов, которые пересчитываются раз в ``10`` секунд в процессе ``quoter`` доходили до целевых ``dns`` инстансов и в итоге результировались в установку ``rate limits`` на ``dnsguard`` каждый инстанс сконфигурирован эти изменения конфигураций получать следующим образом:
* периодический опрос по списку указателей на конфигурации, которые могут быть применены на данном хосте
* постоянный процесс ``watches`` реагирующий на изменения в конкретных конфигурациях 
* каждая нода понимает включена ли она в процесс такого получения изменений (см. режим ``dry-run``)

Конфигурация ``dns`` инстансов задаётся так, в ней указаны конфигурации ``dns`` которые могут быть получены через систему установки лимитов
```yaml
  # TODO: some nodes (or all) could be controlled by
  # configuration mechaincs based on runtime config (e.g. dnsguard)
  # and a list of watches by model watch and sync.
  watches:

    # a d2 client side mechainics that uses
    # watches and periodical syncs to update
    # controlled configurations
    locations: [ "alpha" ]

    # classes and hosts forcefully enabled for auto-configration
    classes: [ "ns+cache" ]

    # fqdn and instances
    hosts: [ "alpha-05v.lxd.tt.yandex.net" ]

    # status file to store the last watches
    # changes (events and periodic syncs) 
    status-file: "/var/tmp/d2-watches.json"

    # root path for configurationm, expecting
    # template /dns-core/config/s/${s}l/${l}h/${h}t/${t}
    root : "/dns-core/config"

    # a list of possible configuration types 
    types : [ "dnsguard" ]
```
В конфигурации указаны жёстко ноды и сервисы которые работают в боевое режиме, остальные в режиме ``dry-run``. Следующие команды определяют оба режима конфигурирования (в соответствии с конфигурацией только нода ``alpha-05v.lxd.tt.yandex.net`` сервиса ``ns-cache`` может быть отконфиугирована)
```sh
    # запускаем на ноде "alpha-05v.lxd.tt.yandex.net" для 
    # периодической проверки -- есть ли изменения в конфигурациях
    # лимитов для нас

    d2 config generic periodic --type="dnsguard" --dry-run --debug

    DEBU[2022/07/30 - 19:06:23.283] [919449]:[1] (config) (generic) (periodic) request to periodic configuration sync 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) get config path:'/dns-core/config/s/ns+cache/l/vla/h/alpha-05v.lxd.tt.yandex.net/t/dnsguard' code:'200' 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [01]/[17] {     
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [02]/[17]    "uuid": "895008af-8111-4421-98f0-584d9dd14281", 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [03]/[17]    "type": "config+dnsguard", 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [04]/[17]    "owner": "dns", 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [05]/[17]    "created": "2022-07-29T17:38:09.883478762+03:00", 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [06]/[17]    "updated": "2022-07-29T17:38:09.883704169+03:00", 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [08]/[17]    "pps_limits": { 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [09]/[17]       "any_project_id": -1, 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [10]/[17]       "per_project_id": { 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [11]/[17]          "0x85612": 1000, 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [12]/[17]          "0x85632": 1103, 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [13]/[17]          "0xdeadbeef": 1000, 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [14]/[17]          "0xf803": 16000 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [15]/[17]       } 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [16]/[17]    }  
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (get) [17]/[17] }     
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] (configs) (processing) received current type:'dnsguard'
        path:'/dns-core/config/s/ns+cache/l/vla/h/alpha-05v.lxd.tt.yandex.net/t/dnsguard'
        config:'uuid:'895008af-8111-4421-98f0-584d9dd14281',type:'config+dnsguard',owner:'dns',
        created:'2022-07-29 17:38:09.883478762 +0300 MSK',created:'2022-07-29 17:38:09.883704169 +0300 MSK'' 
    DEBU[2022/07/30 - 19:06:23.355] [919449]:[1] dnsguard api call:'http://[::1]:8080/api/v1/limit/pps' 
    DEBU[2022/07/30 - 19:06:23.356] [919449]:[1] (configs) (processing) got dnsguard local limits count:'4' 
    DEBU[2022/07/30 - 19:06:23.356] [919449]:[1] (config) (dnsguard) (apply) no actions generated, seems to be SYNCED 
    DEBU[2022/07/30 - 19:06:23.356] [919449]:[1] (exec) (watches) (periodical) finished in '72.504643ms' 
```
здесь видно что конфигурация локальная и из центра соответствуют друг другу, ``no actions generated, seems to be SYNCED``
```sh
    # запускаем на ноде "alpha-05v.lxd.tt.yandex.net" для 
    # watchers на конкретные конфигурации 
    # лимитов для нас

    d2 config generic watch --placement="runtime" --path="/dns-core/config/s/c/dnsguard" \
        --path="/dns-core/config/s/ns+cache/l/vla/h/alpha-05v.lxd.tt.yandex.net/t/dnsguard"  \
        --dry-run --debug

    DEBU[2022/07/30 - 19:11:42.906] [930780]:[1] (config) (generic) (watch) paths:['/dns-core/config/s/c/dnsguard'] 
    DEBU[2022/07/30 - 19:11:42.906] [930780]:[1] (configs) (watch) request to process config 'paths:['/dns-core/config/s/c/dnsguard'], 
        placement:'runtime'' 
```
последняя команда будет ждать изменений в по указанном пути ``zookeeper``

### Управление системой квотирования
Входной точкой системы квот является конфигурация, поддерживаемая и управляемая через ``d2``, а также через ``api`` методы ``d2`` для внешних потребителей. Все объекты конфигурации находятся в кластере ``zookeeper`` под отдельным от остальной конфигурации ``dns`` в поддереве ``/dns-core/config/``. Ключи конфигурации имеют следующие паттерны, которые определяют на какой объект ``dns`` они действуют:
* ``/dns-core/config/s/l/h/t/quotas`` - глобальная конфигурация
* ``/dns-core/config/s/ns+cache/l/h/t/quotas`` - конфигурация определяаемая для сервиса ``ns+cache``
* ``/dns-core/config/s/ns+cache/l/sas/h/t/quotas`` - конфигурация для сервиса ``ns+cache`` локации ``sas``
* ``/dns-core/config/s/ns+cache/l/sas/h/ns01h.name.yandex.net/t/quotas`` - конфигурация для сервиса ``ns+cache`` локации ``sas`` только конкретной ноды **``ns01h.name.yandex.net``**

Конфиг квоты в каждом узле дерева (по каждому пути) выглядит так
```json
{
        "uuid": "180df253-4a96-4dfe-8141-3011182d8f78",
        "type": "config+quotas",
        "owner": "dns",
        "created": "2022-07-24T14:07:54.128872746+03:00",
        "updated": "2022-07-25T11:00:17.022899959+03:00",
        "path": "/dns-core/config/s/l/h/t/quotas",
        "pps_quotas": {
                "per_project_id": {
                        "0x85612": [
                                1000,
                                750,
                                500,
                                250
                        ],
                        "0x85632": [
                                1100,
                                825,
                                550,
                                275
                        ],
                        "0xdeadbeef": [
                                1001
                        ]
                }
        }
}
```
Опуская технические атрибуты, основным содержимым является маппинг внутри ``pps_quotas`` и в настоящий момент реализованы квоты типа ``per_project_id``. Квота для ``projectid`` - это массив из ``[]float64{}`` где первый элемент - это значение ``pps`` квоты, которая выставляется в тот самый ``dnsguard`` ``limit`` для объекта конфигурирования. Если это ``service``, ``service+location`` - то это значение распределяется между всеми нодами ``dns`` инстансов локации с учётом веса каждого инстанса, его живости. Этот уровень квотирования называется **``black``** - срабатывание мониторинга уровня ``black`` означает дропы на нодах. В режиме ``dry-run``, просто превышение этого порога. Остальные элементы массива в убывающем порядке определяют уровни ``red``, ``yellow``, ``green`` и соответственно в таком виде попадают в мониторинг.

Из этого конфига ``квот`` уровня локации (и других подходящих из поиска для ``projectid``) ``quoter`` строит ``лимиты`` распределяя квоту по лимитам вида (лимиты тоже находятся в ``zookeeper``)
```json
{
        "uuid": "7e1ea365-35b8-49d8-ae34-0b04b20a00e4",
        "type": "config+dnsguard",
        "owner": "dns",
        "created": "2022-07-30T19:40:36.698896604+03:00",
        "updated": "2022-07-30T19:40:36.699286037+03:00",
        "path": "/dns-core/config/s/ns+cache/l/vla/h/alpha-05v.lxd.tt.yandex.net/t/dnsguard",
        "pps_limits": {
                "any_project_id": -1,
                "per_project_id": {
                        "0x85612": 1000,
                        "0x85632": 1103,
                        "0xdeadbeef": 1000.4,
                        "0xf803": 16000
                }
        }
}
```

Каждая из конфигураций ``квот`` и ``лимитов`` может изменена быть через ``d2``. Однако, фактически имеет смысл менять входящую конфигурацию только ``квот``, так как лимиты пересчитываются процессом ``quoter`` самостоятельно - он просто перетрёт быстро изменения внесённые вручную.

#### Сценарии управления квотами

**Создание** квоты для ``projectid`` через ``d2``, может быть выполнена на мастерах ``dns-core``
```sh
    # устаналиваем квоты для конкретной ноды ns06e.name.yandex.net 
    # projectid 0x85612 в значение 100, при этом остальные уровни
    # red, yellow, green автоматически проставятся исходя из вектора
    # коэффициентов [0.75, 0.5, 0.25]
    
    d2 config quotas set --service="ns+cache" --host="ns06e.name.yandex.net" 
        --location="iva" --project-id="0x85612" --quota=100 --debug
```
**Листинг** установленных квот в системе:
```sh
    # получаем установленные в системе квоты в виде
    # таблицы, используем для этого generic config
    # методы

    d2 config generic list  --type="quotas" -T
```
**Редактирование** квоты по её пути вручную - то есть конфиг квоты прилетает в редактор и ответственный может внести изменения в текст конфигурации и если она сможет смаршаллится в структуру - она применится в ``zookeeper`` пути
```sh
    # редактируем вручную квоты, тут нужно убедится что 
    # указанный путь существует

    d2 config generic edit --path="/dns-core/config/s/ns+cache/l/vla/h/alpha-05v.lxd.tt.yandex.net/t/dnsguard" --debug
```
**Удаление** квоты:
```sh    
    # убираем квоту, следует убедится что triple 
    # service, location, host имеют соответствующее значение
    # иначе ничего не произойдёт

    d2 config quotas unset --project-id="0x85612" --debug --dry-run
```
В командах ``config quotas`` можно использовать ``triple`` (``service``, ``location``, ``host``) или ``path`` в том виде как себя идентфицирует конфигурация.

#### Мониторинг процесса квотирования

Сами процессы квотирования ``quoter``, ``cooker`` должны также мониторится. Основной метрикой может быть выполняются ли периодически эти процессы как установлено конфигурациями, для этого есть мониторинги:

* [dns-cooker](https://juggler.yandex-team.ru/raw_events/?project=&query=service%3Ddns-cooker) ``['processed metrics:'25':'OK',stalled processing:'7 > 600':'OK',out of frame:'25 > 100':'OK'']`` - определяет текущее состояния процессинга входящих метрик со стороны `dns` инстансов
* [dns-quoter](https://juggler.yandex-team.ru/raw_events/?project=&query=service%3Ddns-quoter) `` ['processed metrics input:'1272' output:'46' ->'OK',stalled processing:'1 > 600':'OK'']`` - показывает как он справляется с переконвертацией квот в лимиты 

#### Внешнее управление квотами
Для возможного внешнего управлениям квотами в коде ``d2`` есть **нереализованные** пока ``placeholders`` для методов кода
```go
// a list of quota methods implementing on
// master side, setting quota via PUT
// editing quota via PATCH, getting and
// listing quotas via GET
authorized.PUT("/quota", a.apiPutQuota)
authorized.PUT("/quota/:projectid", a.apiPutQuota)

// patching quota means setting only some
// properties of quota
authorized.PATCH("/quota", a.apiPatchQuota)
authorized.PATCH("/quota/:projectid", a.apiPatchQuota)

// listing all quota configuration
authorized.GET("/quota", a.apiGetQuota)
authorized.GET("/quota/:projectid", a.apiGetQuota)
```
планируем делать тут (см. тикет  <span style="color:red">**T.B.D.**</span>)
