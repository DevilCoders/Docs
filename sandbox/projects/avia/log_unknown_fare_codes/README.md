Описание задачи
===============

В задаче выполняется проход по дневной таблице avia-variants-log.
Информация о неизвестных `fare_code` и `fare_code`, для которых багаж в сегменте не совпал с багажом в справочнике тарифов,
попадает в `avia-unknown-fare-codes-log`

Задача бинарная, чтобы ее загрузить в локальную песочницу в консоли:
```bash
cd arcadia/sandbox/projects/avia/log_unknown_fare_codes/
ya make --checkout --yt-store .
sandbox upload_binary log_unknown_fare_codes --enable-taskbox --attr released=stable --attr task_type=AVIA_LOG_UNKNOWN_FARE_CODES
```

Для заливки в большой sandbox:
```bash
cd arcadia/sandbox/projects/avia/log_unknown_fare_codes/
ya make --checkout --yt-store .
./log_unknown_fare_codes upload --owner AVIA --attr released=stable --attr task_type=AVIA_LOG_UNKNOWN_FARE_CODES
```
