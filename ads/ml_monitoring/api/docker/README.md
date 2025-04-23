## Разворачивание на yp

Предисловие:

* На yp не выходит поднять докер с сетью. 
Ndp-proxy с налета не вешается, потому что в yp выдается не подсеть, а один айпишник. Наверное, можно сделать туннелирование
* Локально на маке не выходит поднять, потому что на маке `--net host` не работает. 
Если использовать Docker Desktop, то поиграться с подсетью и айпифорвардингом больно - 
при ошибке конфигурации вылетает и требует переконфигурации всего с нуля
* Докер в арке по дефолту не собирается

```bash
~/arc/arcadia/ads/ml_monitoring/api/docker
ilariia@ilariia> make configure_yp
ilariia@ilariia> make run_yp
```

## Разворачивание на ml-dev.search.yandex.net

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

ilariia@ml-dev:~/arcadia/ads/ml_monitoring/api/docker$ ifconfig
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

**Первая причина** - висит старый неприбитый процесс с докером. 
Так как новому докеру начинает выделяться новый адрес в подсети, то нужно пробрасывать новый route на него. Или просто убить старый докер.
Если будет проблемой, можно будет сделать, чтоб автоматом менялись роуты в таблице роутинга.

**Вторая причина** - если еще не сконнектились докер и родительский хост. Проблему решит повторный make docker
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

### Запустить контейнер

```bash
$ make run 
```

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

Подконнектится к докеру

```bash
$ make login
```

Подключить к логам в докере

```bash
$ make logs
```

### Cобрать контейнер для разработки

```bash
$ NIRVANA_TOKEN=<token> make run-dev
```

### Посмотреть swagger

Доступиться к сваггеру можно по линку: http://ml-dev.search.yandex.net:8080/swagger
