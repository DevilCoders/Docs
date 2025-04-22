# Логи сервиса

Логцы можно посмотреть в [логвьювере](https://direct.yandex.ru/logviewer).
Описание таблиц [здесь](../reference/logviewer/tables-description.md).
Подробнее про логвьювер [здесь](../reference/logviewer/quick-start.md)

## Логи от приложений

### Общая схема
![https://jing.yandex-team.ru/files/pe4kin/deploy%20direct.jpg](_assets/direct_apps_logs.jpg "Схема попадания логов")

### Perl
Логцы пишутся из скриптов в файлы и затем подхватываются [push-client](https://docs.yandex-team.ru/unified_agent/migration/migration_from_push_client#push-client) -ом, отправляющим логцы в [logbroker](https://logbroker.yandex-team.ru/docs/overview) согласно [конфигам](https://a.yandex-team.ru/arcadia/direct/packages/yandex-direct-send-logs-to-logbroker).
push-client запоминает i-node-у и позицию в файле(можно ротировать).

Особенности:
Некоторые скрипты пишут логи в файлы с форматом названия <имя>.YYYYMMDD.
Для того, чтобы push-client понимал в Директе есть [скриптик](https://a.yandex-team.ru/arcadia/direct/infra/direct-utils/push-client-linker), который делает линки в отдельную папочку в нужном формате

### Java
Java приложения могут писать в двух форматах, в зависимости от аппендера для log4j и того где запускается приложение:
- в сокет [unified agent](https://docs.yandex-team.ru/unified_agent/) в случае запуска в деплое [конфиг](https://a.yandex-team.ru/arcadia/direct/libs-internal/config/src/main/resources/log4j2-deploy-appenders.xml)
- в файлики в `/var/log` при запуске в nanny, на ppcdev-ах [конфиг](https://a.yandex-team.ru/arcadia/direct/libs-internal/config/src/main/resources/log4j2-development.xml)

В случае записи в файлики они по тому же принципу как в Perl подхватываются push-client-ом.
В случае с UA: [unified agent](https://docs.yandex-team.ru/unified_agent/) слушает на порту 16400, а приложения(и nginx) закидывают в него логцы и он отправляет их в [logbroker](https://logbroker.yandex-team.ru/docs/overview).

### Топики в логброкере
В логброкере для заливки логов настроены [топики](https://logbroker.yandex-team.ru/docs/concepts/resource_model#topic) с именами, мнемонически соотносящимися с логами. Для чтения используется consumer `direct-logshatter2`.
По его read rule-ам можно посмотреть какие топики нам нужны:
- [logbroker](https://logbroker.yandex-team.ru/logbroker/accounts/direct/direct-logshatter2?page=configuration&type=consumer)
- [lbkx](https://logbroker.yandex-team.ru/lbkx/accounts/direct/direct-logshatter2?page=configuration&type=consumer&browserFilter=)

## Логи балансера
![https://jing.yandex-team.ru/files/pe4kin/direct_awacs_logs.jpg](_assets/direct_awacs_logs.jpg "Схема попадания логов балансера")
Логи с подов с балансерами заливаются через push-client в отдельный логброкерный топик, оттуда читаются и парсятся [логфеллером](https://wiki.yandex-team.ru/logfeller/) и заливаюся в YT и кликхаус.
Заливка в кх происходит посредством [data transfer](https://wiki.yandex-team.ru/data-transfer/) :
- [Продовый](https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/data-transfer/transfer/dtt49untf48po1s3ki1f/view) и [тестовый](https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/data-transfer/transfer/dttkhmod803goaagpdgf/view) трансферы.
- [Эндпоинт логфеллера](https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/data-transfer/endpoint/dteimenvo8eai279ctks/view) (источник) указывает из какого [топика]((https://logbroker.yandex-team.ru/logbroker/accounts/direct/awacs-l7-access-log?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics)) читать, а также каким консьюмером(`
/direct/direct-lf-2-clh`) и каким парсером(`district-balancer-log`).
- [Эндпоинт кликхауса](https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/data-transfer/endpoint/dteo8k87pcngpe38pjoa/view) (приемник) с настройкой в какую таблицу писать.

Описание логов можно посмотреть [тут](https://wiki.yandex-team.ru/balancer/logi-v-balansere/)


## Хранение в кликхаусе
Заливка и чтение в кликхаусе происходит через 2 уровня балансировки:
- Специальная самописная прокся над кликхаусами, которая учитывает занятое место на машинках и распределяет запись на свободные, а также предоставляет кликхаусные интерфейсы для чтения. Подробности [тут](https://wiki.yandex-team.ru/jeri/logshatter-in-mds/)
- [L3 балансер](https://l3.tt.yandex-team.ru/service/8678) `ppchouse-cloud.direct.yandex.net` над проксями для организации одной точки входа. Требует периодического передергивания(передеплоя с переуказанием кондукторной группы), т.к. хосты переливаются в няне с новыми ip-шниками, а L3 об этом ничего не знает.

Кластеры в MDB:
- [Продовый](https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/managed-clickhouse/cluster/mdbns84iukrpbke13rul/view)
- [Тестовый](https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/managed-clickhouse/cluster/mdb84apvnr71pbaga50r/view)

## Хранение в YT
Также из логброкера логи читаются и парясятся логфеллером и складываются в YT. Конфиги:
[hahn](https://a.yandex-team.ru/arcadia/logfeller/configs/logs/direct_hahn_logs.json)
[arnold](https://a.yandex-team.ru/arcadia/logfeller/configs/logs/direct_arnold_logs.json).

Лежат на хане и арнольде по пути `//home/direct/logs/`

## Мониторинги
- [Джаглерный агрегат](https://juggler.yandex-team.ru/check_details/?host=direct.prod_subsystems&service=logs&project=direct.prod&last=1DAY) про логи
- [Джаглерный агрегат](https://juggler.yandex-team.ru/check_details/?host=direct.prod_apps-health&service=logshatter&project=direct.prod&last=1DAY) про логшаттер.
- [Документация](../reference/alerts/tm-awacs-ch.md) по мониторингу авксовых логов через дата-трафнсфер.

