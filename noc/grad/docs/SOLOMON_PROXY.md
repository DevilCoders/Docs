Выкатка:

```shell
salt-call state.highstate
```

Перекладывание в stable
```shell
ssh noc.dupload.dist.yandex.ru
find_package -r noc -e unstable solomon-proxy | grep _amd64.deb
sudo dmove noc stable solomon-proxy 1.8.xxx unstable

find_package -e unstable influx-proxy | grep _amd64.deb
sudo dmove noc stable influx-proxy 1.8.xxx unstable
```

Деплой:
```shell
executer p_exec %nocdev-solomon-proxy 'apt-get update>/dev/null ; apt-get install solomon-proxy=1.8.9440764'
```

Кондукторная группа [nocdev-solomon-proxy](https://c.yandex-team.ru/groups/nocdev-solomon-proxy).
Конфиг [nocdev-grad-server.sls](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/nocdev-grad-server.sls)
