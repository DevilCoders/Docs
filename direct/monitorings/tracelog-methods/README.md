# Мониторинг методов по tracelog из clickhouse (пакет yandex-du-slbmon на ppcback)

Файлы из этой директории попадают на ppcback скриптом dt-tracemon-get-configs.
Над ними запускается генератор крон-файлов dt-tracemon-cron-updater
Образовавшиеся крон-файлы запускают dt-tracemon для соответствующих конфигов.

Подробнее:
https://wiki.yandex-team.ru/jeri/tracelog-methods-monitor/
