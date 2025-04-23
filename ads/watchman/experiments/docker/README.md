## Разворачивание watchman на ml-dev.search.yandex.net

### Поставить докер

Пока работает только для xenial. Добавляет репозиторий, выкачивает образ, добавляет нужных людей в docker-группу

```bash
$ make init
```

Статус работы демона:

```bash
$ systemctl list-units --type=service --state=running | grep docker
```

Информация о старте:
```bash
$ journalctl -u docker.service
```

### Сконфигурировать докер

Конфигурирование добавляет поддержку ipv6 к демону
```bash
$ make configure
```
Проверить, что появился Scope:Global ipv6 адрес

```bash

ilariia@ml-dev:~/arcadia/ads/watchman/docker$ ifconfig
docker0   Link encap:Ethernet  HWaddr 02:42:29:ce:9d:bd
          inet addr:172.17.0.1  Bcast:0.0.0.0  Mask:255.255.0.0
          inet6 addr: 2a02:6b8:b000:7119:922b:34ff:fecf:2f81/125 Scope:Global
          inet6 addr: fe80::1/64 Scope:Link
          inet6 addr: fe80::42:29ff:fece:9dbd/64 Scope:Link
```

### Собрать контейнер

Версия выставляется относительно текущего коммита.
Собирается тестовая версия контейнера.
```bash
$ make docker
```
Может появиться ошибка Could not resolve <repository>.

Первая причина - висит старый неприбитый процесс с докером. 
Так как новому докеру начинает выделяться новый адрес в подсети, то нужно пробрасывать новый route на него. Или просто убить старый докер.
Если будет проблемой, можно будет сделать, чтоб автоматом менялись роуты в таблице роутинга.

Другая причина - если еще не сконнектились докер и родительский хост. Проблему решит повторный make docker
```bash
Err http://yabs-precise.bsdist.yandex.net stable/all/ Release.gpg
  Could not resolve 'yabs-precise.bsdist.yandex.net'
Err http://yabs-precise.bsdist.yandex.net stable/amd64/ Release.gpg
  Could not resolve 'yabs-precise.bsdist.yandex.net'
```
Собирает в том числе зависимые бинари:
```bash
$ make docker-all
```
### Создать volume для jupyter

Доступное извне хранилище, которое поддерживается контейнером
```bash
$ make volume
```

Посмотреть на созданные volume:
```bash
$ docker volume ls
DRIVER              VOLUME NAME
local               jupyter-volume
local               models-volume
```

Узнать точку доступа к volume:
```bash
$ docker volume inspect jupyter-volume
```

### Инспектируем все вместе

Включает команды для работы с докером, упомянутые выше. Полезно, чтоб быстро посмотреть статус докер-инфраструктуры
```bash
$ make inspect
```

### Запустить контейнер

Проброс 80го порта важен, так как на нем вешается ui
```bash
$ YT_TOKEN=<zomb_distribution token> make run 
```
Если нет токена, то нужно залогиниться под zomb_distribution и сходить на http://locke.yt.yandex.net/auth

Проверить наличие Scope:Global ipv6 адреса
```bash
root@3d025aea5ec3:/# ip -6 addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 state UNKNOWN qlen 1000
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
148: eth0@if149: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 state UP
    inet6 2a02:6b8:b000:7119:922b:34ff:fecf:2f82/125 scope global nodad
       valid_lft forever preferred_lft forever
    inet6 fe80::42:acff:fe11:2/64 scope link tentative
       valid_lft forever preferred_lft forever
```
### Запустить тесты

```bash
$ make test
```

### Запустить свой скрипт в докере

Скопировать скрипты для запуска из репозитория в volume

```bash
$ make sync
```

Подконнектится к докеру

```bash
$ make login
```

Запустить скрипт

```bash
/watchman# python scripts/BSDEV_67366_01.py
```