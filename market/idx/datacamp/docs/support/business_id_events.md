
## Что это

Механизм сбора метрик по произвольным события в разрезе бизнеса. Из-за большого числа бизнесов (10^7), хранение исходных ивентов в готовых системах мониторинга затруднительно. Поэтому сделан отдельный механизм, хранящий лишь агрегаты.
На текущий момент поддержано 5 видов событий: число ошибок транзакций, число конфликтов блокировок транзакций, число прочитанных из базы строк, число записанных строк в офферные и поисковые таблицы. Для каждого вида события считается топ 100 по бизнесам на окне в 30 минут.

## Cхема работы

1. Данные пишутся в топик лога ([прод](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/controllers-event-log?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&accountsFilter=&browserFilter=&metricsFrom=1658329123429&metricsTo=1658415523429&sortOrder=%22default%22), [тестинг](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/controllers-event-log?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&browserFilter=&metricsFrom=1658329155659&metricsTo=1658415555659&sortOrder=%22default%22)) [кодом в контроллерах](https://a.yandex-team.ru/arcadia/market/idx/datacamp/controllers/lib/event_log_writer/event_log_writer.h). Формат данных: https://a.yandex-team.ru/arcadia/market/idx/datacamp/proto/diagnostics/EventLog.proto?rev=r9752018
2. Топик собирается [логфеллером](https://a.yandex-team.ru/arcadia/logfeller/configs/logs/market_arnold_logs.json?rev=r9754508#L3111). Парсер лога: https://a.yandex-team.ru/arcadia/logfeller/lib/log_parser/market_datacamp_event_log_parser.cpp. Таблицы логфеллера: [тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-event-log-testing), [прод](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-event-log)
3. Агрегаты вычисляются по логфеллеру в [таске] (https://a.yandex-team.ru/arcadia/market/idx/datacamp/routines/lib/tasks/datacamp_statistics.py?rev=r9752018#L16-43) вместе с остальной статистикой хранилища. Результаты попадают в статическую [таблицу] (https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/united/aggregated_event_log)
4. По таблице строится дашборд в datalense https://datalens.yandex-team.ru/jei7ywoc4fhca-top-event-by-business-id
