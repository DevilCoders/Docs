# CDP-FILTER
Читатель лога визитов, данные из которого используются для обогащения данных о клиентах в CDP.
Описание CDP можно прочитать тут - https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/README.md

## Описание
`cdp-filter` - процессинговый сервис, читающий логи визитов, убирающий из них всё лишнее и отправляющий прочитанные данные
"дальше по трубе обработки". Данные которые пишет этот сервис используются в
`cdp-matcher` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-matcher/README.md)).

### Deployment
production - https://deploy.yandex-team.ru/stages/cdp-filter-production

testing - https://deploy.yandex-team.ru/stages/cdp-filter-test

### Какие данные потребляет?
`cdp-filter` логи визитов, которые пишет движок Яндекс.Метрики из консюмера `visit-v2-log-cdp-consumer` в Logbroker. Тут
важно заметить, что лог визитов Яндекс.Метрики "двулик" и существует в виде двух отдельных логов - `visit-v2-log` и `visit-v2-private-log`.
В отличие от всех остальных сервисов в CDP, `cdp-filter` читает данные не из cross-dc инсталляции logbroker (aka lbkx), а
из мультикластерной инсталляции, потому что логи визитов пишутся именно туда. Данные в логе едут в формате event-log.
Нормального описания этого формата не существует в природе, можно постараться понять что-то
[по коду C++ библиотеки](https://a.yandex-team.ru/arc/trunk/arcadia/library/cpp/eventlog) или
[по коду парсера написанного на Java](https://a.yandex-team.ru/arc_vcs/metrika/java/api/logbroker-common/src/java/ru/yandex/metrika/lb/eventlog/EventLogBatchSerializer.java),
который не покрывает всех сценариев и поддерживает только парсинг одного из 4х существующих форматов event-log (чего нам более чем достаточно).
Внутри себя event-log использует protobuf. Схема сообщений для visit-log [лежит вот тут](https://a.yandex-team.ru/arc_vcs/metrika/core/libs/protos/protos/visit/visit.ev).
К сожалению, использовать на прямую это описание proto сообщений не получается из-за проблем с javac, так что по факту
мы используем `message VisitPartial`, описание и объяснение причин существования которого
[лежит тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-filter/proto/web_metrika_core.proto).

### Как обрабатывает данные?
При получении очередного визита, `cdp-filter` проверяет, что визит относится к множеству счётчиков Яндекс.Метрики,
для которых включён CDP (фича `cdp`). Полный список таких счётчиков раз в 10 секунд вычитывается в память из таблицы
`system_data/cdp_counters`. Если визит принадлежит к одному из таких счётчиков, то он запоминается, для того, чтобы
отправить информацию из данного визита на дальнейшую обработку.

Основным смыслом существования данного сервиса по факту является выполнение простой map операции над потоком данных в realtime.
`cdp-filter` фильтрует не нужные данные из лога, уменьшая как количество сообщений в нём, так и количество поле в каждом
сообщении. Несмотря на свою тривиальность, он отделён в отдельный сервис для того, чтобы максимально изолировать этот процесс
от всего остального pipeline обработки данных. Так как логов визитов много (сотни мегабайт в секунду), хочется иметь возможность
сделать много шардов обработки входного лога визитов, не раздувая количество шардов в следующих этапах обработки данных.

### Куда пишет данные?
Данные из визитов пишутся в топик `metrika-client-id-add-topic` (`message MetrikaClientIdAdd`) в формате protobuf -
[схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-processing-common/proto/matching.proto). Одна из важных
функций `cdp-filter` реализуется именно во время записи данных, а именно шардирование. Так как изначальный лог визитов никак
не пошардирован, обработка его в сыром виде нарушала подход, при котором все данные в CDP обрабатываются по шардам. Выходной
топик в свою очередь уже шардирован по `intHash64(FirstPartyCookie)`. Подробнее про причины такого шардирования можно
почитать [в описании сервиса `cdp-matcher` тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-matcher/README.md).


## Графики
Графики для production:
1. [Мониторинг консюмера `visit-v2-log-cdp-consumer` в Logbroker](https://logbroker.yandex-team.ru/logbroker/accounts/metrika/visit-v2-log-cdp-consumer)
2. [Мониторинг топика `metrika-client-id-add-topic` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/metrika-client-id-add-topic)
