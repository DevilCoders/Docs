# wiki-yang-downloader
Утилита для обработки заданий из YANG и заливки MRC

Заливать с `spica.maps.dev.yandex.net` (spica) в mrc-agent-proxy (есть дырка до продакшена)

## Запуск утилиты wiki-yang-downloader
Утилита выполняет следующие действия:
1) Загружает для заданного $POOL_ID выполненные задания из yang (http-api)
2) Дампит данные с ненулевыми колонками (если включена опция actions=dump)
3) Синхронизирует записи с заданиями в social-базу НК (таблица yang.assignment)
4) Загружает в память аттачменты из yang (если необходима заливка в MRC)
5) Загружает в MRC результаты заданий - фидбэк с фотаками (если включена опция actions=upload)
6) Синхронизирует результаты (соответствие id задания и id-ки фоток в MRC) в social-базу НК (таблица yang.assignment_photo)

Различаются типы объектов (object kind) и кастятся к [типам MRC](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/mrc/backoffice/backoffice.proto?rev=r8163939#L29):
* address -> ObjectType::ADDRESS_PLATE
* barrier -> ObjectType::BARRIER
* entrance -> ObjectType::BUILDING_ENTRANCE
* passway -> ObjectType::FOOT_PATH

Все остальное отправляется как ObjectType::OTHER

### Опции
| Опция | Описание |
|---|---|
| config <filename> | Путь до config.xml |
| syslog-tag <value> | ид-к для логгера в докере |
| status-dir <dir> | Путь до статус-файла в докере |
| pool-id <n> | Id-к пула из yang ($POOL_ID) |
| actions <value> | Actions: dump - распечатка данных, upload - заливка в MRC, archive - архивация, list - список закрытых пулов, готовых к обработке, help (по умолчанию) |
| tvm-alias <value> | TVM-алиас для отправки в MRC фидбэка с фотками |
| project-id <n> | Идетификатор проекта в yang (по умолчанию: 11361) |
| batch-limit <n> | Просессинг <n> закрытых пулов (обязательно actions=upload,archive) |

### Переменные окружения
#### YANG_TOKEN
Для работы утилиты необходима переменная окружения YANG_TOKEN - OAuth токен для доступа к YANG по http-api.

Значение в https://yav.yandex-team.ru/secret/sec-01daxh7yb9xzd4j5tr4b3t3vvt
(доступно для robot-wikimap)


## Докер
В докере tasks_sprav значение YANG-токена берется из файла /etc/yandex/maps/wiki/secrets/tokens/robot-wikimap-yang-token

Запуск по крону только в `stable` в 20:00 ежедневно.


## Вспомогательные разработческие скрипты в папке scripts/
### Testing, Stable
`$STAGING` - testing или stable

* На spica поднят tvmtool и настроен tvm-alias от tasks-sprav: `maps-core-nmaps-tasks-sprav-$STAGING`
* Нужно создать свой локальный конфиг, не коммитить, настроить доступ в базы (social)
`maps/wikimap/mapspro/cfg/services/services.$STAGING.$USER.xml`

### Описание
* Вспомогательные скрипты для запуска утилиты `tool-$STAGING.sh` - можно адаптировать под себя<br/>
 Пример запуска:
`YANG_TOKEN=<токен вида AQAD-$$$$$$$> ./tool-stable.sh <ид пула: 123456>`
* Вспомогательный скрипт для запуска утилиты в batch-режиме `tool-stable-batch.sh` - обработка пулов и архивация, лучше запускать в `screen` или `nohup`<br/>
 Пример запуска:
`YANG_TOKEN=<токен вида AQAD-$$$$$$$> ./tool-stable-batch.sh <кол-во пулов: 100500>`
