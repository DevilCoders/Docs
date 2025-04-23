
### База данных для Jobs

Сейчас всех сред база данных - ydb. 
Путь к базе - 
dev7: https://ydb.yandex-team.ru/db/ydb-ru-prestable/direct/dev7/hourglass/browser<br>
devtest: https://ydb.yandex-team.ru/db/ydb-ru-prestable/direct/devtest/hourglass/browser<br>
testing: https://ydb.yandex-team.ru/db/ydb-ru-prestable/direct/test/hourglass/browser<br>
прод: https://ydb.yandex-team.ru/db/ydb-ru/direct/production/hourglass/browser<br>
структура таблиц и работа с ними аналогична базе mysql<br>
[описание](https://a.yandex-team.ru/arc/trunk/arcadia/direct/schemata/ydb/hourglass/)

### Примеры запросов
В меню Source можно поменять БД на подходящую из [конфига](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf?rev=6479928#L1082) в формате `{cluster}/{db_name}`

Поиск по имени джобы: https://yql.yandex-team.ru/Operations/YLdMtxJKfYEUq1oxvU2PhR4z01jBwP50DrRmhelqNMA=<br>
Версия расписания в базе: https://yql.yandex-team.ru/Operations/YLdM2hJKfYEUq1pWPQTNiWXtt2uLLeaz0jXMKHl0s_4=<br>
Все инстансы шедулера с временем пинга не больше 5 минут назад: https://yql.yandex-team.ru/Operations/YLdM9RJKfYEUq1pvqmgGnvQhhHOvQ0ujvGE3OsMn8Uw=<br>
Все инстансы, помеченные как главные - https://yql.yandex-team.ru/Operations/YLdNHQuEIw3FdrUtsYi-1MWonDd_4-lxI9GiaFOqJOg=<br>

Документация по ydb - https://ydb.yandex-team.ru/docs/<br>
Метрики по базе лежат на вкладке Metrics у базы(например, https://ydb.yandex-team.ru/db/ydb-ru-prestable/direct/devtest/hourglass/metrics)<br>

график исопльзования пула сессий (тс) - https://solomon.yandex-team.ru/?project=direct-test&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.sensor=ydb_sessions_*&graph=auto&l.env=devtest&l.hourglass_scheduler=HourglassApp
