## Быстрый старт

### Получаем доступ
Сначала стоит проверить, может быть доступ уже есть, потому как для большей части
ноков он выдан изначально. Пробуем открыть [морду swagger](https://test.racktables.yandex-team.ru/v1/swagger/index.html) если получилось - 
доступ есть. Если нет - [IDM](https://idm.yandex-team.ru/system/rt-staging-ctl/roles/profile#f-status=all,f-role=rt-staging-ctl,sort-by=-updated)
ждет тебя.


### Как поставить
#### Скачать
   * [linux](https://test.racktables.yandex-team.ru/v1/client/linux)
   * [mac](https://test.racktables.yandex-team.ru/v1/client/mac)
   * [freebsd](https://test.racktables.yandex-team.ru/v1/client/freebsd)
   * [windows(untested)](https://test.racktables.yandex-team.ru/v1/client/win)
Если не работает или не получилось или просто не хочется - можно собрать самостоятельно.
#### Для linux
```
# ставим go по инструкции https://docs.yandex-team.ru/arcadia-golang/getting-started
git clone git@noc-gitlab.yandex-team.ru:nocdev/rt-docker.git
cd rt-docker/noc/rttestctl/cmd/rttctl/
make build
cp rttctl ~/bin/ # или куда-нибудь в $PATH
```
#### Как поставить MacOS
```git clone git@noc-gitlab.yandex-team.ru:nocdev/rt-docker.git
cd rt-docker/noc/rttestctl/cmd/rttctl; brew install go; brew install make
make localinstall;
~/go/bin/rttctl nodes
```
#### Для остального
...

### токен
[rttctl gettoken](rttctl_gettoken.md) - основной способ, либо
руками получить токен [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5a70922036fa453f9b881142f21c4df8)

### Как использовать
[rttctl spawn](rttctl_spawn.md) - самый нужный сценарий

#### Полезняшки
```shell script
rttctl help completion
# RTTCTL_HOST указывает точку входа в api, позволяет прицепится к любой ноде напрямую.
export RTTCTL_HOST=n4.test.racktables.yandex-team.ru
export RTTCTL_TOKEN=AQAD-...
mkdir -p ~/.config/rttctl && echo $RTTCTL_TOKEN  > ~/.config/rttctl/token
# фильтр '--node name=$NODE_NAME' указывает на какой ноде запускать окружение
# то есть если не указать RTTCTL_HOST то подключение к кластеру стейджинг хостов может произойти не через n4
# а если не указать фильтр `--node name=n4...` то окружение может подняться не на n4
rttctl spawn --node name=n4.test.racktables.yandex-team.ru
rttctl ps --node name=n4.test.racktables.yandex-team.ru # берём UUID нашего окружения
# rttctl ssh выдает на stdout команду подключения по ssh, примерно как 'ssh -t -p 2222 nN.test.racktables.yandex-team.ru rt-fpm UUID'
`rttctl ssh UUID-окружения`
```



