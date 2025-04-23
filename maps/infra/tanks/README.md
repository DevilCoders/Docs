# Tanks

[RTC: сервис для нагрузочного тестирования (стрельб) (GEOINFRA-1424)](https://st.yandex-team.ru/GEOINFRA-1424)

Карточные танки. Используются для карточных стрельб в RTC.

Большинство карточных сервисов стреляются в DC MAN, поэтому сервис содержит 3 танка в MAN и по одному в SAS и VLA.  

Танки в RTC заведены по инструкции: [Яндекс.Танк#HowTo](https://wiki.yandex-team.ru/Load/howto/TankHowTo/?from=%252Fnagruzochnoetestirovanie%252Fhowto%252FTankHowTo%252F)

Так как сервис не использует базовый образ карт, Golovan панель поправлена вручную, чтобы показывать только метрики Proto. 

## Usage

Для использования танков достаточно в sandbox таске SHOOT_VIA_TANKAPI добавить параметр `Shooting parameters -> List of tanks: nanny:maps_core_tanks_load`

Пример шедулера с карточными танками: https://sandbox.yandex-team.ru/scheduler/13424/view

Подробнее про регрессионное тестирование: [Пошаговая инструкция по созданию сервисов в RTC#Настроить регулярное регрессионное тестирование](https://wiki.yandex-team.ru/maps/dev/core/instrukcija-po-sozdaniju-servisov-v-rtc/#nastroitreguljarnoeregressionnoetestirovanie)

## General information

| Key | Value |
|---|---|
| Сервис в ABC | [maps-core-tanks](https://abc.yandex-team.ru/services/maps-core-tanks) |
| Tracker Queue | <https://st.yandex-team.ru/GEOINFRA> |

## Instances

| Environment | URL |
|---|---|
| Load | <https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_tanks_load/> |

## Monitorings

| Staging | Juggler panel |
|---|---|
| Load | <https://juggler.yandex-team.ru/?query=host%3Dmaps_core_tanks_load> |

## Logs

Логи сервиса стрельб искать в контейнерах в Няне.

| | |
|---|---|
| Tank | `/place/db/www/logs/yandex-tank/tankapi/*` |
