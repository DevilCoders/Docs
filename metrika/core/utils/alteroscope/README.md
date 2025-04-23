# alteroscope

Утилита генерации альтеров для АппМетрики. На вход получает альтер и список ssqls-ок.

Получить токен для бишопа https://docs.yandex-team.ru/bishop/api

Добавление колонок
```
./alteroscope -s metrika/core/libs/appmetrica/tables/fields/RevenueEvent.ssqls -a "ADD COLUMN RevenueValidationEnvironment Enum8('undefined'=0, 'production'=1, 'testing'=2) AFTER RevenueOrderIdSource" -o packages -v error -t ~/.arc/token -e testing
```

Удаление колонок
```
./alteroscope -s metrika/core/libs/appmetrica/events_writer/tables/NotificationEvent.ssqls metrika/core/libs/appmetrica/events_writer/tables/PushTokenEvent.ssqls -a "DROP COLUMN IF EXISTS NetworksInterfaces.Names, DROP COLUMN IF EXISTS NetworksInterfaces.Macs" -o packages -v error -t ~/.arc/token -e testing
```

Как работает
- По ssqls определять зависимые программы
- Ходит за их конфигами в Bishop https://bishop.mtrs.yandex-team.ru
- Если не находит, то ходит по машинам за `/etc/<program>/config-preprocessed.xml`
- Понимает по конфигам пишушие таблицы и кластеры КХ
- По движку таблицы строит граф зависимостей между таблицами
- Генерирует альтер для всех зависимых таблиц в виде команды executer'а
- Генерирует команду проверки альтера
- Может вывести список программ для пересборки

Список команд
```
./alteroscope --help
usage: alteroscope [-h]
                   [-v [{info,information,warn,warning,critical,error,debug,fatal}]]
                   -s SSQLS_PATHS [SSQLS_PATHS ...] -a ALTER
                   [-e {production,testing}] [-o {packages}]
                   [-t TOKEN_FILE_NAME]

optional arguments:
  -h, --help            show this help message and exit
  -v [{info,information,warn,warning,critical,error,debug,fatal}], --verbose [{info,information,warn,warning,critical,error,debug,fatal}]
                        verbose level (default: None)
  -s SSQLS_PATHS [SSQLS_PATHS ...], --ssqls SSQLS_PATHS [SSQLS_PATHS ...]
                        ssqls paths relative Arcadia root (default: None)
  -a ALTER, --alter ALTER
                        example: -a "ADD COLUMN ClientIPHash UInt64 AFTER
                        ClientIP" (default: None)
  -e {production,testing}, --environment {production,testing}
                        default testing (default: testing)
  -o {packages}, --output {packages}
                        show dependent packages (default: None)
  -t TOKEN_FILE_NAME, --token_file_name TOKEN_FILE_NAME
                        user token (default: ~/.arc/token)

For example
./alteroscope -s metrika/core/libs/appmetrica/tables/fields/RevenueEvent.ssqls -a "ADD COLUMN RevenueValidationEnvironment Enum8('undefined'=0, 'production'=1, 'testing'=2) AFTER RevenueOrderIdSource" -o packages -v error -t ~/.arc/token -e testing

./alteroscope -s metrika/core/libs/appmetrica/events_writer/tables/NotificationEvent.ssqls metrika/core/libs/appmetrica/events_writer/tables/PushTokenEvent.ssqls -a "DROP COLUMN IF EXISTS NetworksInterfaces.Names, DROP COLUMN IF EXISTS NetworksInterfaces.Macs" -o packages -v error -t ~/.arc/token -e testing
```

Пример работы
```
drobus@drobus:~/arc/metrika/core/utils/alteroscope$ ./alteroscope -s metrika/core/libs/appmetrica/tables/fields/RevenueEvent.ssqls -a "ADD COLUMN RevenueValidationEnvironment Enum8('undefined'=0, 'production'=1, 'testing'=2) AFTER RevenueOrderIdSource" -o packages -v error -t ~/.arc/token -e testing
[2020/04/13-19:20:46][metrika.pylib.bishop][ERROR]: Config not found for any environments
config-preprocessed.xml                                                                                                      100%   11KB  11.1KB/s   00:00
[2020/04/13-19:20:58][metrika.pylib.bishop][ERROR]: Config not found for any environments
config-preprocessed.xml                                                                                                      100%   19KB  19.1KB/s   00:00
[2020/04/13-19:21:00][metrika.pylib.bishop][ERROR]: Config not found for any environments
config-preprocessed.xml                                                                                                      100% 6198     6.1KB/s   00:00
[2020/04/13-19:21:02][metrika.pylib.bishop][ERROR]: Config not found for any environments
config-preprocessed.xml                                                                                                      100% 9997     9.8KB/s   00:00
============ Dependent packages ===============================
columnar-appender-mobile
decoded-crashes-export
decoded-crashes-import
mobile-demo-data
mobile-clickbuffer-writer
mobile-giga-events-writer
mobile-logs-api-import-server
mobile-logs-api-import-uploader
mobile-massive-destinations-writer
mobile-statbox-events-writer
revenue-events-validator

============ Original alters ==================================
====== Replicated tables
p_exec %mtmobgiga-test,-mt.*-[2|3]t?\..* for table in mobile.revenue_events; do echo "kill query where elapsed > 100;ALTER TABLE $table "'ADD COLUMN RevenueValidationEnvironment Enum8('"'"'undefined'"'"'=0, '"'"'production'"'"'=1, '"'"'testing'"'"'=2) AFTER RevenueOrderIdSource' | clickhouse-client --multiquery || { code=$?; echo "failed at table $table" ; exit $code; } ; done
p_exec %mtmoblog-test,-mt.*-[2|3]t?\..* for table in mobile.revenue_events; do echo "kill query where elapsed > 100;ALTER TABLE $table "'ADD COLUMN RevenueValidationEnvironment Enum8('"'"'undefined'"'"'=0, '"'"'production'"'"'=1, '"'"'testing'"'"'=2) AFTER RevenueOrderIdSource' | clickhouse-client --multiquery || { code=$?; echo "failed at table $table" ; exit $code; } ; done
====== check
p_exec %mtmobgiga-test,-mt.*-[2|3]t?\..* for table in mobile.revenue_events; do echo "SELECT RevenueValidationEnvironment from $table LIMIT 0" | clickhouse-client --multiquery || { code=$?; echo "failed at table $table" ; exit $code; } ; done
p_exec %mtmoblog-test,-mt.*-[2|3]t?\..* for table in mobile.revenue_events; do echo "SELECT RevenueValidationEnvironment from $table LIMIT 0" | clickhouse-client --multiquery || { code=$?; echo "failed at table $table" ; exit $code; } ; done

====== Distributed tables
p_exec %mtmoblog-test for table in mobile.{revenue_events_all,revenue_events_layer}; do echo "kill query where elapsed > 100;ALTER TABLE $table "'ADD COLUMN RevenueValidationEnvironment Enum8('"'"'undefined'"'"'=0, '"'"'production'"'"'=1, '"'"'testing'"'"'=2) AFTER RevenueOrderIdSource' | clickhouse-client --multiquery || { code=$?; echo "failed at table $table" ; exit $code; } ; done
====== check
p_exec %mtmoblog-test for table in mobile.{revenue_events_all,revenue_events_layer}; do echo "SELECT RevenueValidationEnvironment from $table LIMIT 0" | clickhouse-client --multiquery || { code=$?; echo "failed at table $table" ; exit $code; } ; done

============ Materialized alters ==================================
============ Possible alters ==================================
```
