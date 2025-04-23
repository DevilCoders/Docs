# Сервисные YQL-запросы

## select_possible_head_offline.sql
Поиск ГУ, у которых возможны проблемы с интернетом.

Параметризированный запрос:

* `$start_date` - (`YYYY-MM-DD`) начальная дата расчёта
* `$end_date` - (`YYYY-MM-DD`) конечная дата расчёта
* `$cooldown_date` - (`YYYY-MM-DD`) дата в таблице `$tagged_cars`, ранее которой машина считается "остывшей" и может быть помечена повторно
* `$tagged_cars` - путь до таблицы, в которой хранятся записи о помеченных машинах
* `$calculation_days` - количество дней, участвующих в расчёте (соответствует количеству дней от `$start_date` до `$end_date`)

[Пример запуска](https://yql.yandex-team.ru/Operations/XjK-qmHljp3WY4FO6EELyMwfg3HuXZCePNku7bZNITE=) с установленными параметрами.
