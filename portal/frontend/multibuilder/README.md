## Сборка нового релиза

```
dch -i
debuild
dupload yandex-multibuilder_<version>_amd64.changes -t common
```

Для сборки нужны пакеты `devscripts` и `dupload`. Также нужен рабочий и привязанный к стаффу GPG-ключ.

`common` - специальное имя из конфига dupload
Можно сделать примерно такой конфиг в домашней папке:
~/.dupload.conf
```
package config;

$default_host = "common";

$cfg{'common'} = {
    fqdn => "common.dupload.dist.yandex.ru",
    method => "scpb",
    incoming => "/repo/common/mini-dinstall/incoming/",
    dinstall_runs => 0,
};
```
