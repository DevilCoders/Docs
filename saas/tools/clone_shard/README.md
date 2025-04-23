## `clone_shard`

### Что это?
Инструмент для того, чтобы склонировать себе инстанс саасного сервиса и запустить/подебажить его. Копируются конфиги, индекс по ssh, а затем формируются скрипты для сборки и запуска rtyserver'a.

### Как это запустить?
`./clone_shard [-h] [-d DESTINATION_PATH] [-i SKIP_DOWNLOADING_INDEX] [-t HOST] [-s SERVICE] [-c CTYPE] [-p PORT]`

Пример запуска:
`./clone_shard --destination-path /home/odinmillion/education --host saas-yp-education-2.vla.yp-c.yandex.net --port 24000`

### Артефакты работы

* `build.sh` - скрипт для сборки rtyserver'a. Перемещает собранный бинарь в destination-path. Нужна переменная окружения $ARCADIA.
* `run.sh` и `debug.sh` - скрипты для запуска и дебага.
* `index, logs, state, config` и прочее - артефакты, скопированные в рамках работы утилиты.

### Hints

* Может быть полезно выключить DM в конфиге, чтобы сервер на старте не перетирал ваши конфиги скаченными из DM'a: `DaemonConfig.Controller.DMOptions.Enabled : 0`
* Также можно выключить DOCFETCHER, чтобы запускать на замороженном индексе: `Server.ModulesConfig.DOCFETCHER.Enabled: false`
* Т.к. индекс скачивается по ssh, могут быть проблемы из-за мержей.

