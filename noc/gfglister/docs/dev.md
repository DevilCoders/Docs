Конфигурация:
```yaml
gfglister:
  http_address: "[::]:80" # тут слушаем запросы
  invapi_filter: "[работает gfglister]" # фильтр хостов
comocutor:  # параметры для получения конфига через get_config
  login: "robot-gfglister"
  identity_path: "/path/to/robot-gfglister"
zk:
  hosts: [ "host1" ]
  prefix: "/gfglister"
  timeout: 10s
invapi:
  oauth: "token"
  url: "https://ro.racktables.yandex-team.ru/api"
svn:
  svn_ssh: "ssh -i /etc/gfglister/id_dsa"
  url: "svn+ssh://arcadia.yandex.ru/robots/trunk/noc/cfglister/gfglister_config"
  work_dir: "/path/to/gfglister"
```
Сервис обслуживает только хосты из фильтра `invapi_filter`. Есть автоматика, которая обновляет конфиги, если они давно не обновлялись.

Для отказоустойчивости используется zookeeper и лок. Тот кто держит лок тот главный и только он отвечает
балансерем ненулевым весом. Остальные отвечают нулевым и, следовательно, не получают вебхуки.

Получение конфигов процесс нетривиальный и состоит из трех попыток. Вызов get_config (обертка над comocutor) под gfglister.
Если не удалось, например из-за swdev, то используется аннушка под racktables и последний вариант аннушка под racktables с туннелем и паролем.

Если были изменения структур под ```//easyjson:json```, то вызываем go generate:
```shell
ya tool go generate -v -x ./...
```

Сервис запущен на группе [nocdev-gfglister](https://c.yandex-team.ru/groups/nocdev-gfglister). Выкатка конфигов:
```shell
executer p_exec %nocdev-gfglister "salt-call state.highstate queue=true"
```
Код лежит в [noc/gfglister](https://a.yandex-team.ru/arc/trunk/arcadia/noc/gfglister). Выкатка через conductor настроена в CI.
Тестинг не предусмотрен.

### TODO:
- История комментов хранится только у мастера, а значит рестарт или переключение сбрасывает её.
