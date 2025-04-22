# Правила именования серверов, балансеров и кондукторных групп

## Именование серверов

Происходит по следующему принципу:
**host**-**number**-**dc**.**env**.vertis.yandex.net

Часть | Описание
:---: | :---:
host | Имя хоста/кластера, например "front" или "mysql", допускается двойное имя хоста, например "mysql-slave"
number | Порядковый номер хоста. Может начинаться без нуля(1,3,4, etc)
dc | Трёхбуквенное имя датацентра, общепринятое в Яндексе: sas/vla/man/myt.
env | Окружение, в котором находится хост: prod/dev/test

Например:

* cassandra-realtime-01-man.test.vertis.yandex.net
* mysql-master1-5-vla.dev.vertis.yandex.net
* telepony-api-011-sas.test.vertis.yandex.net
* telepony-controller-01-myt.test.vertis.yandex.net

Конвенция именования хостов одинаковая для железных серверов и виртуалок.


## Именование кондукторных групп

Координаты:

* Проект, в котором живут все группы - [vertis](https://c.yandex-team.ru/projects/vertis/);
* Корневая группа - [vertis](https://c.yandex-team.ru/groups/vertis).

Название группы строится из названия корневой группы + название среды + название самой группы.

Среды: **prod**, **vprod**, **test**, **vtest**, **dev**, **vdev**.
Название группы: название самой группы, которое может, в свою очередь иметь ветвление и деление.

Все железные хосты заводятся только в среды: **prod**, **test** и **dev**.
Все виртуальные хосты (lxc,kvm,docker, yandex-cloud) заводятся только в среды: **vprod**, **vtest** и **vdev**.

Таким образом всегда должно быть возможно получить, например, все хосты корневой группы **vertis**, или, например,
все железячные хосты **%vertis_prod,%vertis_dev,%vertis_test**, или все хосты продакшна, железные и виртуальные: **%vertis_prod,%vertis_vprod**

Разделителями всегда является символ подчёркивания "_", тире, дефисы и т.д. не допускаются, дабы не создавать путаницы в файрволлах, cauth и т.д.,
т.к. там все символы принудительно заменяются на символ подчёркивания.

Примеры названий групп:
**vertis_prod_back**
**vertis_dev_back_auto**
**vertis_test_back_realty**
**vertis_vprod_octopus**
**vertis_vdev_nodejs_travel**

## Именование NOC-SLB

Мы разделяем NOC-SLB по назначению:

* Для внешнего трафика;
* Для внутреннего трафика, который проходит через lb-int(envoy);
* Для внутреннего трафика не через lb-int(envoy).

Схема именования такая:

Назначение | Схема
:---: | :---:
Внешний трафик | **name**-ext.noc-slb.**env**.vertis.yandex.net
Внутренний трафик через noc-slb(envoy) | **name**-int.vrts-slb.**env**.vertis.yandex.net
Внутренний трафик | **name**-int.noc-slb.**env**.vertis.yandex.net

env может быть test или prod.

Примеры названий NOC-SLB:

* autoru-front-ext.noc-slb.prod.vertis.yandex.net
* envoy-api-int.vrts-slb.test.vertis.yandex.net
* service-int.noc-slb.test.vertis.yandex.net
