# ytbootstrap - наливатор БД в YT

ytbootstrap делает начальную копию данных из таблиц MySQL в YT

### Пример запуска 

    java -cp binlogbroker-ytbootstrap.jar:binlogbroker-ytbootstrap/'*' \
         ru.yandex.direct.binlogbroker.ytbootstrap.YtBootstrap \
         --mysql-include-tables campaigns \ 
         --mysql-exclude-tables addresses \
         --yt-cluster hahn --yt-path //tmp/direct/user/
         --shards ppc:1,ppc:2

Параметры `--mysql-include-tables` и `--mysql-exclude-tables` определяют какие таблицы копировать. Если `--mysql-include-tables` не задан, будут выбраны все таблицы в базе, за исключением указанных в `--mysql-exclude-tables`.
 
Как запустить тестовый MySQL в Docker - см. [direct/libs/binlog-event](direct/libs/binlog-event/README.md)
