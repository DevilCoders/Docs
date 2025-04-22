# Типовое решение подключения Mac Mini

Статья описывает типовое решение подключения устройств Mac Mini к сети ДЦ. 

Автор: [Вадим Воловик](https://staff.yandex-team.ru/vdvolovik)

Текущее количество устройств MacMini: 1500. 

План на 2022 год: 250.

## Предпосылки решения

[Mac Mini](https://www.apple.com/ru/mac-mini/) включается в сеть ДЦ, потому что по правилам компании Apple сборка программного обеспечения должна производиться на устройствах Apple, а так как серверов Apple не выпускает, то компания Yandex ставит устройства Mac Mini для разработчиков iOS. Наливка Mac Mini производится через Internet Recovery.

## Описание решения

Mac Mini требуют подключения "медными" портами, а также на них нельзя применить стандартные правила FW из-за особенностей программного обеспечения Mac Mini. Для нормальной работы проектов с Mac Mini необходимо обеспечить взаимодействие:
- Mac Mini <----> Mac Mini (между проектами)
- Mac Mini <----> Internet
- Mac Mini <----> Server Tech Admin

В схеме подключения участвуют:
1. Mac Mini
2. Switch - коммутатор с медными портами для подключения устройств Mac Mini

  {% cut "Требования к коммутатору..."}
  
  - Uplinks: 2x10GE Optic
  - Downlinks: 24-32-48 1xGE Couper

  {% endcut %}

3. Router Guppy -  роутер, обеспечивающий FW и маршрутизацию для устройств Mac Mini

  {% cut "Требования к Router Guppy" %}

  - CPU: XEON-1512
  - RAM: 16 Gb
  - SSD: 2

  {% endcut %}

4. ToR - см. [Глоссарий:ToR](https://docs.yandex-team.ru/nocdoc/glossary#t)
5. Server Tech Admin - сервер с Init-конфигурации Mac Mini.
6. IPMI Switch

_Схема HLD_
![Схема HLD](./images/img1.png)

### LLD Решения

- MacMini подключается портом в access-порт коммутатора Small Switch. На порт MacMini назначается:
  - IPv4-адрес из диапазона `192.168.X.X/26`, с помощью DHCPv4
  - IPv6-адрес из /96 сети, выделенной для VLAN, привязанного к Project Id проекта
  - Для IPv6 назначается `default gw` `fe80::1`
- На коммутаторе Small Switch настраиваются VLANs
- На Router Guppy:
  - Fib.3
    - Настраиваем на UPLINK в сторону ToR:
      - VLAN 688
      - IPv6 link-local
      - Default gw via ToR
    - Для IPv4 подключения MacMini:
      - DHCPv4
      - CLAT
    - Для IPv6 подключения MacMini:
      - Вешаем на VLAN IPv6 с хостовой частью
    - Настраивается правила iptables
  - Fib.0 (Mgmt):
    - Настраиваем iBGP до Rybka для OAM

![](./images/MacMini_Integration_0.04-LLD.jpg)

{% note alert %}

Тем командам, которые уже работают с MacMini из общего project_id, предстоит пройти процедуру выделения [нового project_id](https://docs.yandex-team.ru/nocdoc/processes/project_id/get_new_project_id/about), а также предстоит изменить IPv6 адреса устройств.

{% endnote %}

### Требования по физическому подключению Mac Mini

- Mac Mini подключается к сети одним медным 1GE портом.
- В один юнит стойки помещается два Mac Mini.
- В одну стойку помещается 48 Mac Mini, поэтому необходимо предусмотреть установку 48-портового коммутатора
- Для подключения Mac Mini обязательно использовать устройство Router Malek, выполняющий функции NAT64 и FW.

Целевая схема организации физического подключения оборудования в стойке:

_Схема физического подключения оборудования в стойке_
![Схема физического подключения оборудования в стойке](./images/img2.png)

## Процедура подключения Mac Mini

Шаг 1. Устройство подключается к коммутатору, подключается питание.

**Если требуется Recovery**
Шаг 2. Устройство включается в режиме Recovery.
Шаг 3. Устройство получает IPv4 адрес по DHCP, который настроен на Router Malek
Шаг 4. Устройство идет в интернет для загрузки Recovery образа.
Шаг 5. Устройство перезагружается и готово к работе с IPv6.

Если не требуется Recovery - Шаг 2-5 пропускается.

Шаг 6. На Small Switch активируется VLAN.
Шаг 7. На Mac Mini настраивается IPv6 Link-Local адрес.
Шаг 8. На Router Malek применяются правила FW. Настраивается статическая маршрутизация.

## Запуск схемы

- **Заведение тикета.** В очередь NOC необходимо завести задачу на подключение MacMini
  ```
  Заголовок: Подключение MacMini по целевой схеме.

  ДЦ: IVA|MYT|MAN|SAS|VLA
  Стойка: {Номер стойки}
  Количество MacMini: 12
  Список Project Id:
    - 1
    - 2
    - 3
  ```
- **Поиск железа**:
  - Guppy смотрим в [bot:guppy](https://bot.yandex-team.ru/umka/list?filter=attrs:%257B%2522SRV.SERVERS%2522%253A%257B%2522attribute11%2522%253A%255B%2522GIGABYTE%2522%255D%252C%2522attribute16%2522%253A%255B%25221%2522%255D%252C%2522attribute17%2522%253A%255B%2522INTEL%2520XEON%2520D-1521%2522%255D%257D%257D;room_type:DC%252CENGINEERING%252COFFICE%252CWAREHOUSE;group_by_location:false;planner_id_neq:false;nomenclature:SRV%253ESERVERS), заводим задачу на ITDC на установку сервера с необходимыми параметрами.
  - Коммутатор (switch) также смотим в [bot:switch](https://inventory.yandex-team.ru/items/21846), заводим задачу на ITDC на установку коммутатора коммутатора с необходимыми параметрами
- **Коммутация оборудования**
  - MacMini подключаются к Switch 1GE портом
  - Switch подключается 10GE Uplink в Router Guppy
  - Router Guppy подключаентся 10GE Uplink в ToR
- **Наливка switch**
- **Наливка Router Guppy**


[Ссылка на схему]({{scheme.drawio.url}})

## Описание работы скрипта

{% include notitle [Путь до описания](./README.md) %}