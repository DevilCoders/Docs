Утилита для визуализации статистки по вызовам маршрутов.
````
usage: route_stats [-h] [-d DATE_RANGE DATE_RANGE] [-s STARTING_DAY] [-u]

optional arguments:
  -h, --help            show this help message and exit
  -d DATE_RANGE DATE_RANGE, --date-range DATE_RANGE DATE_RANGE
                        The first and the last date of a range to export data in format 'YYYY-MM-DD'. Both boundaries are included.
  -s STARTING_DAY, --starting-day STARTING_DAY
                        The starting point of the horizontal axis. The starting day is between 0 and 100
  -u, --update-all-data
                        Export data from the database. Don't use this flag if you've already exported data

````
Данная утилита собирает статистику по кол-ву вызовов маршрутов(за диапозон дней,
заданный через `--data-range`)
на i-ый день после дат этих маршрутов.
По умолчанию берётся статистика за последние 7 дней.

Всего выводятся четыре графика

название                     |файл                      |комментарий
-----------------------------|--------------------------|--------------
% запросов от глубины истории|percent_request_prefix.png|Считает сколько процентов запросов приходится на i дней после даты маршрута
кол-во запросов после определённого дня|cnt_request_suffix.png|Вычисляет кол-во запросов маршрутов после i-го дня с момента дат этих маршрутов
% уникальных путей за день от глубины истории|percent_uniq_route_prefix.png|Пусть `stat[i]` - кол-во маршрутов, вызванных в i-ый день. Тогда график показывает `100 * sum(stat[:i+1]) / sum(stat)`
кол-во запросов на день|request.png|кол-во запросов на i-ый день после даты маршрута

Флаг`--starting-day` помогает определить начало оси X в графиках. Если значение не определено,
дни на оси будут начинаться с 10.

Данные о маршрутах берутся из локального файла. Чтобы получить данные из базы данных, используется `--update-all-data`
Рекомендуется не использовать часто `--update-all-data`, так как это создаёт нагрузку на сервер




