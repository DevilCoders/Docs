# Проблемы

## Сервис не стартует

### Нет данных
Сервис не стартанет, если отсутствуют данные по магазинам. Имеется два пути доставки данных: статический ресурс и загрузка через Market Access. Настраиваются переменными в конфиге, соответственно:
`shops-storage-cache.static-resource-*`
`resource-updater.access-updater.*`

Любой из вариантов можно отключить.

Статический ресурс загружается единожды при старте сервиса. Динамический - периодически. При ошибке загрузки статического ресурса будет предпринята загрузка динамического.
В первую очередь необходимо смотреть основной лог сервиса (`/app/log/market-shops/server.log` или в графане). Ошибки загрузки динамического ресурса Market Access могут быть связаны с проблемами в Access Agent (лог `/app/log/access-agent/common.log`) или Access Updater (в логе сервиса).

Access Updater реализован библиотекой userver market-resource-updater, в лога сообщения фильтруются: `module LIKE '%libraries/market-resource-updater%'%`

Пример ошибки подключения к Access Agent (`/app/log/market-shops/server.log`):

`Failed to create session: 'NMarket.NAccessAgent.IAgentService/CreateSession' failed: code=DEADLINE_EXCEEDED, message='Deadline Exceeded', details='', will be repeated`

Ошибка загрузки ресурса, при исчерпании свободного места (`/app/log/access-agent/common.log`):

`2022-07-05T10:47:33+0300	pid=3824	DBUG	PMQ dequeue NMarket.NAccessAgent.TVersionDownloadAttemptDone (17461a2c61c94922a9954edfe565f780): 1
2022-07-05T10:47:33+0300	pid=3824	INFO	Consumer controller: Consumer 'market-shops' has download done with 'report_shops_data:2116.0.0
2022-07-05T10:47:33+0300	pid=3824	INFO	Consumer updater: Consumer 'market-shops' current changes: modified: resource[report_shops_data].in_download[2116.0.0].error: "(yexception) Skynet \'sky get -d /tmp/access-sample/pdata/access-agent/download/report_shops_data/2116.0.0 -p --progress-format=json --priority High rbtorrent:f67beef3171f94f3a9bbadd59f9b9b6ee583cb70\' returns error (10): {\"done\": false, \"stage\": \"create_handle\"}\n{\"done\": true, \"stage\": \"create_handle\"}\n{\"stage\": \"subproc_started\"}\n{\"done\": false, \"stage\": \"subproc_connect_master\"}\n{\"done\": true, \"stage\": \"subproc_connect_master\"}\nError: FilesystemError: No space left on device {13052:22903}\n" -> "(yexception) Skynet \'sky get -d /tmp/access-sample/pdata/access-agent/download/report_shops_data/2116.0.0 -p --progress-format=json --priority High rbtorrent:f67beef3171f94f3a9bbadd59f9b9b6ee583cb70\' returns error (10): {\"done\": false, \"stage\": \"create_handle\"}\n{\"done\": true, \"stage\": \"create_handle\"}\n{\"stage\": \"subproc_started\"}\n{\"done\": false, \"stage\": \"subproc_connect_master\"}\n{\"done\": true, \"stage\": \"subproc_connect_master\"}\nError: FilesystemError: No space left on device {13052:30395}\n"
modified: resource[report_shops_data].in_download[2116.0.0].done_time.seconds: 1657007199 -> 1657007253
2022-07-05T10:47:33+0300	pid=3824	ERRR	Target controller: Version 'report_shops_data:2116.0.0' download error: (yexception) Skynet 'sky get -d /tmp/access-sample/pdata/access-agent/download/report_shops_data/2116.0.0 -p --progress-format=json --priority High rbtorrent:f67beef3171f94f3a9bbadd59f9b9b6ee583cb70' returns error (10): {"done": false, "stage": "create_handle"}
{"done": true, "stage": "create_handle"}
{"stage": "subproc_started"}
{"done": false, "stage": "subproc_connect_master"}
{"done": true, "stage": "subproc_connect_master"}
Error: FilesystemError: No space left on device {13052:30395}`
