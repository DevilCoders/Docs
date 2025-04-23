# Metridat

## Сервис metridat-collector
Прием двух типов телеметрии:
1. JTI - слушаем UDP-сокет и принимает protobuf от juniper.
2. GNMI - подключение к свитчам по GRPC и получение метрик.

![arch](https://jing.yandex-team.ru/files/gescheit/metridat1.png)

## Сервис metridat-client
Получает данные из LB и записывает их в solomon/graphite.
Про протоколы [telemetry](https://wiki.yandex-team.ru/aleksandrbalezin/telemtry/).

![arch](https://jing.yandex-team.ru/files/gescheit/Metridat.jpg)
## Сервис metridat-aggregator
Получает данные из LB проводит агрегацию/фильтрацию и отсылает результат в solomon или в вебхуки.
![arch](https://jing.yandex-team.ru/files/gescheit/Metridat%20%281%29.jpg)

## Сборка
Регенерация easyjson
```
make easyjson
```
Регенерация protobuf-биндингов
```
make pyproto
```

## Администрирование
conductor [группа metridat-collector](https://c.yandex-team.ru/groups/nocdev-metridat-collector) \
conductor [группа metridat-client](https://c.yandex-team.ru/groups/nocdev-metridat-client) \
Конфигурация [metridat-collector](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/units/metridat-client/files/etc/metridat-collector) \
Конфигурация [metridat-client](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/units/metridat-client/files/etc/metridat-client) \
[Графики client](https://monitoring.yandex-team.ru/projects/grad/dashboards/mon2ihisiui4bbj2tfq3?range=1d&refresh=60)

Выкатка:
```shell
sudo dmove noc stable metridat-client 1.0.0-xxx unstable
executer p_exec %nocdev-metridat-client "salt-call state.highstate"
executer p_exec %nocdev-metridat-client "apt-get update && apt-get install metridat-client"
```
aggregator:
```shell
sudo dmove noc stable metridat-aggregator 1.0.0-xxx unstable
executer p_exec %nocdev-metridat-aggregator "salt-call state.highstate"
executer p_exec %nocdev-metridat-aggregator "apt-get update && apt-get install metridat-aggregator"
```
