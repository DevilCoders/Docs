# Генерация подсетей для докер контейнеров в кластере номада

## Про project_id
[Что такое project_id и как с ним работать](https://wiki.yandex-team.ru/noc/newnetwork/hbf/projectid/)

TLDR: мы живем в project_id сетях, в которых IPv6 адрес состоит из 4 битовых полей:

	|  prefix  |  geo-часть | PROJECT_ID | host-часть |
	|  40 бит  |  24 бита   | 32 бита    | 32 бита    |

  * prefix - это константа, которая указывает на то, что в IP-адресе есть поле PROJECT_ID.
  * geo - поле, где записан идентификатор сети (маршрутизаторы находят путь к этой сети по значению ##prefix + geo##).
  * host-часть - идентификатор хоста внутри пары ##сеть + project_id##.

## Про генерацию подсетей на железных машинках

Железные машинки наливаются с двумя сетевыми интерфейсами: `ethX` и `vlan688`.
При этом:
1) IPv6 адрес на интерфейсе `ethX` принадлежит нашим сетевым макросам `_VERTISPRODNETS_` ( для прода ) и `_VERTISDEVNETS_` ( для dev-a и тестинга ) и ничем не отличается от обычных наших IPv6 адресов.
2) Адрес на интерфейсе `vlan688` принадлежит `VM hbf net` ( отдельному vlan-у с номером `688`, созданному специально для запуска контейнеров ) и имеет вид: `XXXX:XXXX:XXXX:XXXX::badc:ab1e/64` ( где `XXXX:XXXX:XXXX:XXXX` - блоки с prefix-ом и geo-частью )

Так как docker контейнеры должны запускаться во `vlan688`, на каждой машинке мы генерируем подсети для них, таким образом:
- первые 64 бита берем из адреса на `vlan688`
- следующие 32 бита ( PROJECT_ID часть ) копируем из адреса с `ethX`
- первую `/112` подсеть из оставшейся host части (последние 32 бита, `/96` ) отдаём под сеть для контейнеров (т.е. меняем host часть на `:0:1/112` )

Для бесшовного переезда на IPAM плагин ( [https://st.yandex-team.ru/VOID-1478](https://st.yandex-team.ru/VOID-1478) ), нам нужна вторая подсеть для docker контейнеров, её способ генерации аналогичен текущему способу, с отличием в том, что для контейнеров выделяем другую `/112` подсеть: `:f:1/112`

Пример:
Адрес на eth0:    `2a02:6b8:c02:764` `:8000:4098:` `72f1:a701`
Адрес на vlan688: `2a02:6b8:c14:252a` `::` `badc:ab1e`

Подсеть для docker контейнеров: `2a02:6b8:c14:252a` `:8000:4098:` `0:1/112`
Подсеть для IPAM плагина:       `2a02:6b8:c14:252a` `:8000:4098:` `f:1/112`

# Про генерацию подсетей на машинках в ЯОблаке

В каждой зоне (дц) нам выделены `/96` подсети, при этом IPv6 адреса из первой `/112` подсети должны принадлежать виртуальным серверам, все остальные `/112` подсети можно отдавать под контейнеры.

Для удобства эксплуатации, IPv6 адреса виртуальных машинок мы генерируем по шаблону ( подробнее [тут](https://wiki.yandex-team.ru/vertis-admin/klaster-nomada-v-j`andeksoblake/) ):
`<subnet>` `:0:` `<prefix><instance.index>`
Где:
`<subnet>` - подсеть в которой запускается виртуалка (без host части в 32 бита)
`<prefix>`  - буквенный префикс, для разограничения разных кластеров в одной сети, у кластера докер-а это `a`
`<instance.index>`  - порядковый номер виртуальной машины кластера в этом ДЦ

Сети для докер контейнеров генерируем исходя из адреса машинки, меняя последние два блока (по 16 бит) местами.

Для бесшовного переезда на IPAM плагин ( [https://st.yandex-team.ru/VOID-1478](https://st.yandex-team.ru/VOID-1478) ), нам нужна вторая подсеть для docker контейнеров, её способ генерации аналогичен текущему способу, с отличием в том, что меняем буквенный префик на `f`

Пример:
Адрес первой виртуальной машины: `2a02:6b8:c02:900:1:d` `:0:` `a1`
Подсеть для docker контейнеров на ней: `2a02:6b8:c02:900:1:d` `:a1:` `0/112`
Подсеть для IPAM плагина:              `2a02:6b8:c02:900:1:d` `:f1:` `0/112`

