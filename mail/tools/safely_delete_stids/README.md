# Скрипт для безопасного удаления "ненужных" stid'ов из MDS

## Описание

Основной тикет по решаемой проблеме: MAILDLV-1877

При запуске вычитывает с помощью `timetail` строки из указанного лога за указанное время, ищет
сообщения вида `should delete stid = <stid>` и выгребает оттуда stid'ы для удаления, пропуская
"шареные" stid'ы (средняя часть которых = `mail:0`). Для каждого пользователя (uid которого берётся
из средней части стида, `mail:<uid>`) его stid'ы помещаются в таблицу `mail.storage_delete_queue`,
откуда потом удаляются с удалением в MDS специальной машинерией.

При помещении стида в таблицу хранимкой проверяется, что его нет в `mail.messages`

## Пакетирование

Сейчас собираются 3 пакета, отличия только в параметрах вызова `safely_delete_stids`:
* `-prod` - для mxback, mxfront и yaback
* `-corp` - для mxbackcorp и mxcorp
* `-nsls` - для dlvcorp

## Запуск

```
usage: safely_delete_stids [-h] -l LOG_FILE [-t TIME] -f {common,syslog} -s
                           SHARPEI_HOST

Check log file and save unneeded stids into mail.deleted_queue

optional arguments:
  -h, --help            show this help message and exit
  -l LOG_FILE, --logfile LOG_FILE
                        Logfile for search unneeded stids in
  -t TIME, --time TIME  Time interval(seconds) to perform search for
  -f {common,syslog}, --timefmt {common,syslog}
                        Log time format for timetail (use "syslog" for fastsrv
                        and "common" for NSLS)
  -s SHARPEI_HOST, --sharpei-host SHARPEI_HOST
                        Sharpei base url
```
