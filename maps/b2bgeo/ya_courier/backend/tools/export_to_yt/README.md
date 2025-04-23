Утилита для экспорта данных из внутренних таблиц YCB в YT.

```
usage: export_to_yt [-h] [--date DATE] [--date-from DATE_FROM] [--date-to DATE_TO] [--entities ENTITIES] --yt-dir
                    YT_DIR [--yt-token YT_TOKEN] [--pg-password PG_PASSWORD]

Utility to export enities from YCB database to YT.

optional arguments:
  -h, --help            show this help message and exit
  --date DATE           Date in format 'YYYY-MM-DD'.
                        Required only for route related entities.
                        Default: yesterday.
  --date-from DATE_FROM
                        First date of a range to export data in format 'YYYY-MM-DD'.
                        Must be used with --date-to. Both dates are included.
                        If set --date is ignored.
  --date-to DATE_TO     Last date of a range to export data in format 'YYYY-MM-DD'.
                        Must be used with --date-from. Both dates are included.
                        If set --date is ignored.
  --entities ENTITIES   Comma-separated entities to export.
                        Possible values: ['company', 'courier', 'depot', 'depot_instance', 'garage', 'order', 'route', 'route_node', 'user'].
                        Default: all
  --yt-dir YT_DIR       YT directory
  --yt-token YT_TOKEN   YT Authorisation token
  --pg-password PG_PASSWORD
                        Postgres database password
```

Скрипт работает в двух режимах:
* Ежедневная выгрузка. Используется для выгрузки сущностей за конкретную дату. Для использования этого режима должен быть задан параметр `--date`.
* Выгрузка за период. Используется для выгрузки данных за заданный период. Для исползования этого режима необходимо задать параметры `--date-from` и `--date-to`, при этом параметр `--date` игнорируется.

Скрипт генериурет следующие таблицы:

| Тип сущности   | Таблица                             |
| -------------- | ----------------------------------- |
| Отдельные сущности                                   |
| company        | `yt_dir/companies`                  |
| courier        | `yt_dir/couriers`                   |
| depot          | `yt_dir/depots`                     |
| user           | `yt_dir/users`                      |
| Сущности по маршрутам (режим ежедневной выгрузки)    |
| depot_instance | `yt_dir/depot_instances/YYYY-MM-DD` |
| garage         | `yt_dir/garages/YYYY-MM-DD`         |
| order          | `yt_dir/orders/YYYY-MM-DD`          |
| route          | `yt_dir/routes/YYYY-MM-DD`          |
| route_node     | `yt_dir/route_nodes/YYYY-MM-DD`     |
| Сущности по маршрутам (режим выгрузки за период)     |
| depot_instance | `yt_dir/depot_instances`            |
| garage         | `yt_dir/garages`                    |
| order          | `yt_dir/orders`                     |
| route          | `yt_dir/routes`                     |
| route_node     | `yt_dir/route_nodes`                |

Таблицы сущностей, связанных с маршрутами, создаются с временем жизни в 180 дней.
