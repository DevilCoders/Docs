# FAQ по ситуациям в дежурстве

{% note info %}

Здесь будем собирать основные происшествия и часто задаваемые вопросы и ссылки на их решения, происходящие во время дежурств

{% endnote %}

## Поиск
При любой непонятной ситуации не стесняйтесь искать в интранете. Особенно помогает поиск по тикетам:
- по очереди DirectAdmin [сслыка на поиск](https://search.yandex-team.ru/stsearch?text=&facet.queue=DIRECTADMIN)
- по очереди Direct [сслыка на поиск](https://search.yandex-team.ru/stsearch?text=&facet.queue=DIRECT)

Поиск по документации достаточно хорошо работает. Поле ввода запроса для поиска находится вверху этой страницы, примерно тут ↗.
Не стесняйся спрашивать коллег, найти список ответственных за подсистемы можно [здесь](../reference/who-knows.md)

## Базовые операции

### Релизы


  - сборка релиза [java в NewCI](../guide/releases/release-newci.md), [perl-а](../guide/releases/perl.md) и [dna](../guide/releases/dna.md)
  - выкладка в [NewCI](../processes/regulations_deploy_releases_newci.md), [perl](https://wiki.yandex-team.ru/jeri/app-duty/releases/#vykladkareliza-perl), [dna](https://wiki.yandex-team.ru/jeri/app-duty/releases/#vykladkareliza-dna)
  - откат в [NewCI](../jeri/guide/deploy.md)
  - релизные тикеты
    - миграции
    - зависимости
  - лимтесты
  - [окна](../concepts/releases/deploy-schedule.md) выкладок
  - тесты

### Где найти приложения:
приложения продовые/непродовые живут в двух системах деплоя Nanny(conductor и его группы в качестве инвентори) и Deploy. В каких конкретно стейджах в деплое или сервисе в няне обычно понятно из названия сервиса. В сервисе это знание хранится в [репозитории](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/zk-sync/confs/direct-apps.conf.yaml) с обязательной синхронизацией в зукипер.
Там находим приложение, например, `java-alw`, в секции этого приложения ищем раздел `conductor_groups` для приложений в няне или `yadeploy-stages` для приложений в деплое. Состав хостов в кондукторной группе можно посмотреть в кондукторе `https://c.yandex-team.ru/groups/<название группы>`. По именам(до цифры) хостов можно отфильтровать название сервиса в Няне.

### Управление трафиком

- Изменение весов ДЦ - количества трафика, которое будет попадать в ДЦ [дока](../jeri/howto-dc-l7.md)
- Перестать принимать запросы конкретным подом:
  - [переналить его](../jeri/howto-redeploy-pod.md)(самый хороший вариант, не требует захода на машинку, но теряется стейт и возможность дебага)
  - JAVA: подсунуть файлик `/tmp/java_alive.force_down` - это заставит приложение отдавать в ручке `/alive` не 200й код, что приведет к снятию анонса
  - PERL: остановить веб-сервис(direct-accel на фронтах, intapi-direct-accel и soap-direct-accel на интапи и апи соотв.) на машинке

### Проверки

Проверки и способы починки описаны в доке:
- [Каталог проверок](../reference/alerts/example.md)
- [Каталог джоб](../reference/jobs/list/Template.md)(проверки генерятся из самих джоб и имеют их названия)
- [Perl экспорт в БК/perl-scripts(частично)](../reference/bs-export-diag.md)

## Нестандартные ситуации

- Долгий запрос в БД:
  - Посмотреть Query ID: `dbs-innotop pr:<...>`
  - Получить план по этому ID:
`
ppcback$ sudo -u ppc dbs-sql pr:ppc:18 "explain for connection ${QUERY_ID}\G"
`
  - Получить сам запрос: `dbs-sql pr:ppc:9 'show full processlist\G' | grep -A1000 ${QUERY_ID}\G' | sed -z 's/\n\*\{20,\}.*/\n/'`

{% cut "пояснение про grep и sed" %}

`grep -A1000` -- вернёт строку с нужным текстом и следующие 1000 строк (`-A` означает "after")

До `sed` результат будет выглядеть примерно так:
`
           Id: 27807841
         User: ppc
         Host: direct-perl-scripts-sas-yp-1.sas.yp-c.yandex.net:52480
           db: ppc
      Command: Query
         Time: 9457
        State: Sending data
         Info: SELECT /* reqid:216649852448520990:direct.script:ppcResendDomainsBS */ reverse(b.reverse_domain) as domain
                , ifnull(ft.filter_domain, reverse(b.reverse_domain)) as filter_domain
                FROM banners b
                    LEFT JOIN filter_domain ft on ft.domain = reverse(b.reverse_domain)
                WHERE b.reverse_domain IS NOT NULL
                    AND 1
                GROUP BY b.reverse_domain
                ORDER BY null
    Rows_sent: 0
Rows_examined: 0
*************************** 56. row ***************************
           Id: 27816536
         User: direct-ro
         Host: ppcdev6.yandex.ru:52785
<...>
`

`sed` обрежет строку, начинающуюся с череды символов `*` и всё, что встретит дальше

Останется только наш запрос:
`
           Id: 27807841
         User: ppc
         Host: direct-perl-scripts-sas-yp-1.sas.yp-c.yandex.net:52480
           db: ppc
      Command: Query
         Time: 9457
        State: Sending data
         Info: SELECT /* reqid:216649852448520990:direct.script:ppcResendDomainsBS */ reverse(b.reverse_domain) as domain
                , ifnull(ft.filter_domain, reverse(b.reverse_domain)) as filter_domain
                FROM banners b
                    LEFT JOIN filter_domain ft on ft.domain = reverse(b.reverse_domain)
                WHERE b.reverse_domain IS NOT NULL
                    AND 1
                GROUP BY b.reverse_domain
                ORDER BY null
    Rows_sent: 0
Rows_examined: 0
`

{% endcut %}

- Переключение мастера mysql [Дока](../guide/jeri/mysql-change-master.md)
- Кончается место в базе:
  - Посмотреть на графике, например, [15 шард](https://solomon.yandex-team.ru/?project=internal-mdb&cluster=mdb_mdb375dkr3no5kk4bigg&service=mdb&host=sas-59lotys41wcqitwl.db.yandex.net&node=by_host&sensor=*_%2Fvar%2Flib%2Fmysql&node=by_host&graph=auto&threshold=&stack=false&b=7d&e=) имя кластера взять [тут](https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/managed-mysql?section=list)
  - [Статистика](https://direct.yandex.ru/logviewer/short/q10mPQ_a5AhpZ4) по пишущим методам, нужно только выбрать свои даты
  - [Статистика](https://direct.yandex.ru/logviewer/short/vrn3y5VQ5AhqkM) по INSERT-ам в таблицы, нужно только выбрать свои даты
- Протух токен Аудиторий `password.expire_time.yndx-robot-direct-aud` - обновить пароль роботу, перевыпустить токен, записать свежее в yav и [обновить](../jeri/guide/yadeploy-add-secrets.md) его в деплое
- Создание топиков/консьюмеров и других штук в LogBroker [Дока](../guide/jeri/lb-create-objects.md)
- Перезагрузить контейнер в Nanny/Deploy [Дока](../jeri/howto-redeploy-pod.md)
- Посмотреть логи
  - [Логвьювер](https://direct.yandex.ru/logviewer)
- Включение/изменение фичи `#TODO`
- Старт остановка джоб [Дока](../reference/jobs/jobs-common.md)
- Добавить секрет в прод
  - [в деплое для java](../jeri/guide/yadeploy-add-secrets.md)
  - для [перла](https://a.yandex-team.ru/arcadia/direct/packages/secrets/yandex-dau-secrets-direct-prod/etc/yandex/yav-deploy/direct-production.conf) и обновить пакет
  - для [ТС](https://a.yandex-team.ru/arcadia/direct/packages/secrets/yandex-dau-secrets-direct-test/etc/yandex/yav-deploy/direct-testing.conf) и обновить пакет
- Обновление с даунтаймом в груте - см. тикеты [1](https://st.yandex-team.ru/DIRECT-161511) [2](https://st.yandex-team.ru/DIRECT-163989)
- база на ppcdev на localhost `sudo service mysql.unittests start`
- нет логцов от приложений - осознать [доку](../jeri/logs-pipeline.md) и проверить что мого было отсохнуть

### Добавить ситуацию в этот список

Если не хочется коммитить, но хочется сообщить о интересном кейсе во время дежурства - заполни [формочку](https://forms.yandex-team.ru/surveys/107744/)
