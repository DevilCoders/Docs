# USERPARAMS-SHARDER
Шардер параметров посетителей

## Описание
Основное назначение: шардирование топика с параметрами посетителей, который пишет движок. Шардирует по `userId` и пишет в другой топик, который читает `userparams2d`.

Также в шардированный топик `faced` пишет параметры посетителей, загруженные напрямую пользователями через API.

При процессинге вычищаются невалидные (пустые) данные + есть возможность семплирования по `userId`.

### Читает:
топик `userparams-log`

[тестинг](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/test/userparams/userparams-log?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1637773463861&metricsTo=1637859863861&sortOrder=%22default%22)

[прод](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/userparams/userparams-log?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1637776226013&metricsTo=1637862626014&sortOrder=%22default%22)

консьюмер `userparams-sharder`

[тестинг](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/test/userparams/userparams-sharder?page=statistics&type=consumer&tab=readMetrics&metricsFrom=1637776353424&metricsTo=1637862753424&sortOrder=%22default%22)

[прод](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/userparams/userparams-sharder?page=statistics&type=consumer&tab=readMetrics&metricsFrom=1637776300138&metricsTo=1637862700138&sortOrder=%22default%22)

[формат protobuf](https://a.yandex-team.ru/arc_vcs/metrika/java/api/management-common/proto/userparams.proto)
### Пишет:

топик `userparams-sharded-log`

[тестинг](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/test/userparams/userparams-sharded-log?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1637776389332&metricsTo=1637862789332&sortOrder=%22default%22)

[прод](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/userparams/userparams-log?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1637776418826&metricsTo=1637862818826&sortOrder=%22default%22)

[формат protobuf](https://a.yandex-team.ru/arc_vcs/metrika/java/api/management-common/proto/userparams.proto)

### Графики

[тестинг](https://solomon.yandex-team.ru/?project=metrika&cluster=userparams-sharder&service=userparams-sharder&l.env=testing&l.sensor=userparamsSharderProcessor.*)

[прод](https://solomon.yandex-team.ru/?project=metrika&cluster=userparams-sharder&service=userparams-sharder&env=production&sensor=userparamsSharderProcessor.*)

Метрики:
1. `EmptyParams` - количество отфильтрованных пустых параметров (пустой путь/значение)
2. `SampledParams` - количество отсемплированных параметров
3. `FullFilteredMessages` - количество сообщений, в которых все параметры оказались отфильтрованы
