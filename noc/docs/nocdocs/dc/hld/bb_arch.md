# Архитектура магистральной сети

Идеология магистральной сети предполагает, что устройства, образующие IP/MPLS ядро (отдельно стоящие [P-маршрутизаторы](https://racktables.yandex-team.ru/index.php?andor=and&cft%5B%5D=516&cfe=&page=depot&tab=default) и [Edge-коммутаторы](https://racktables.yandex-team.ru/index.php?page=depot&tab=default&andor=and&cfe=%7B%24typeid_8%7D&cft[]=1379) внутри ДЦ), не участвуют в BGP и не обладают информацией о внешних IPv4/IPv6 маршрутах. Их роль сводится к форвардингу трафика от одного PE-устройства к другому по MPLS-метке.

В роли PE-устройств выступают [бордеры](https://racktables.yandex-team.ru/index.php?andor=and&cft%5B%5D=57&cfe=&page=depot&tab=default) и устройства внутри ДЦ, которые терминируют VRF-ы (Spine1, D).
Эти маршрутизаторы связаны друг с другом оптическими линками, арендованными каналами или через DWDM и создают 2 отдельные друг от друга сущности, две сети: [Backbone](http://cacti-noc.yandex.net/plugins/weathermap/weathermap-cacti-plugin.php?action=viewmap&id=dc3dd752b90ed19d1485) и [Fastbone](http://cacti-noc.yandex.net/plugins/weathermap/weathermap-cacti-plugin.php?action=viewmap&id=1d7aa359cc8b314202bd).

**Backbone** - по ней передается пользовательский и прочий "интерактивный" трафик, для которого критичны задержки и потери.

**Fastbone** - предназначена для служебного трафика, не столь критично относящегося к увеличению задержки и потерям. По сети Fastbone стоит передавать bulk-трафик:
- вроде репликации баз данных
- передачи логов.

По сети Backbone передавать критический сервисный тафик с минимизацией потерь и задержек.

Для создания LSP и распространения транспортных меток используется LDP для Fastbone и связка LDP/RSVP для Backbone.
Поддержка IPv6 в ядре отсутствует, поэтому информация о привязке сервисных MPLS-меток к различным маршрутам (IPv6/VPNv6) распространяется по BGP с помощью labeled IPv6-префиксов, с IPv4 BGP Next Hop и технологий 6PE [RFC4798](http://tools.ietf.org/html/rfc4798) и 6VPE [RFC4659](https://tools.ietf.org/html/rfc4659).

Между PE-маршрутизаторами эту информацию распространяют BGP Route Reflector-ы.

[Список BGP Route Reflector](https://wiki.yandex-team.ru/noc/reflectors/)

## Механизм выбора между BB и FB

На PE-маршрутизаторах внутри ДЦ запущено два OSPF процесса, в каждый из которых включены соответствующие линки - или BB, или FB. В каждый процесс добавлен loopback-интерфейс.
Для того, чтобы удаленные PE, могли верно выбрать искомый интерфейс, PE анонсирует префиксы, добавляя уникальный атрибут Next Hop, равный [IPv6 IPv4-mapped](https://tools.ietf.org/html/rfc4291#section-2.5.5) адресу loopback-интерфейса в зависимости от BGP-community маршрута - `::FFFF:<BB IPv4 loopback>` или `::FFFF:<FB IPv4 loopback>`.

_Пример политики:_
```
<vla1-1d2>dis cu int LoopBack
#
interface LoopBack0
 ip address 95.108.237.255 255.255.255.255
#
interface LoopBack10
 ip address 10.255.0.13 255.255.255.255
#
<vla1-1d2>dis cu configuration route-policy SET_VPN_NHOP
#
route-policy SET_VPN_NHOP permit node 10
 if-match community-filter REANNOUNCE_COMMUNITY
 if-match extcommunity-filter MATCH_VPN_COMM_BB
 apply ipv6 next-hop ::FFFF:95.108.237.255
#
route-policy SET_VPN_NHOP permit node 20
 if-match community-filter REANNOUNCE_COMMUNITY
 if-match extcommunity-filter MATCH_VPN_COMM_FB
 apply ipv6 next-hop ::FFFF:10.255.0.13
#
route-policy SET_VPN_NHOP permit node 30
 if-match ipv6 address prefix-list PFXS_SPECIALv6
 if-match community-filter TOR_ANYCAST_COMMUNITY
 if-match extcommunity-filter MATCH_VPN_COMM_BB
 apply ipv6 next-hop ::FFFF:95.108.237.255
#
```

## Дизайн Route Reflector

На текущий момент имеется несколько разных типов RR: IPv4, 6PE, VPN, LUARR подробнее будет описано тут:....
