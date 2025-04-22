# Стрельбы

## Подготовка

- Создаём тикет в Трекере на стрельбы и создаём стрельбу для него (Действие > Нагрузочное тестирование). После этого появится связанный тикет из [Лунапарка](https://lunapark.yandex-team.ru).
- Заходим в [стрессовый инстанс Коннекта](https://qloud-ext.yandex-team.ru/projects/workspace/portal/stress2)
- Ставим туда пакет с актуальной версией.

## Генерация патронов

Запускаем команду `npm run ammo`. На выходе получим файл `cartridges.ammo` в корне репозитория.

## Запуск стрельб

Переходим в [Лунапарк](https://lunapark.yandex-team.ru) и заходим в тикет, для которого создавали стрельбу.
Выбираем _Пострелять_ в шапке сервиса и заполняем поля необходимые для стрельбы:

**Мишень**: идём в [стрессовый инстанс Коннекта](https://qloud-ext.yandex-team.ru/projects/workspace/portal/stress2) и из компонента `back` берём название хоста в Qloud (например, `sas1-698e8c963e9d.qloud-c.yandex.net`).
**Задача** (task): номер таска (например, `DIR-2716`).
**Схема нагрузки**: смотрим [доку](https://yandextank.readthedocs.io/en/latest/tutorial.html#first-steps) и выбираем подходящую.
**Патроны**: выбираем и загружаем из файла, сгенерированного ранее.
**Имя стрельбы**: даём уникальное название для стрельбы.

В редактор внизу страницы нужно добавить строку `use_tank=<TANK_HOST>`. `<TANK_HOST>` &mdash; это хост машины, с которой мы будем стрелять по танку. Его можно посмотреть в окружении [portal-shooting-ground](https://qloud-ext.yandex-team.ru/projects/workspace/portal/shooting-ground/portal-shooting-ground), в информации о компоненте `portal-shooting-ground` выбираем хост инстанста с типом `tank` (например, `sas1-89592b2c4329.qloud-c.yandex.net`).

Чтобы запустить стрельбу, нажимаем кнопку _Огонь!_.

## Документация

- [Стрельбы](https://wiki.yandex-team.ru/nagruzochnoetestirovanie/lunapark/Firestarter/#povtoritstrelbu)
- [Танк](https://yandextank.readthedocs.io/en/latest/index.html)

## Конфигурация окружений в Qloud

**/workspace/portal/stress2**

Variables:
```
CONNECT_ENVIRONMENT=stress
CONNECT_API__DIRECTORY=https://api.stress.directory.ws.yandex.ru
CONNECT_API__BLACKBOX=http://pass-stress-s1.sezam.yandex.net/blackbox
CONNECT_API__PDD=http://pdd-back-loadtest.cmail.yandex.net/iapi
CONNECT_TOKENS__PDD=Static NnT0kyavvF00eH9Z
CONNECT_APP__LOG_LEVEL=debug
TZ=Europe/Moscow
NOOP=2
```

Domains:
portal-stress.ws.yandex.ru
portal-stress2.ws.yandex.ru

**/workspace/portal/shooting-ground**

Variables:
```
DIRECTORY_API=http://api.stress.directory.ws.yandex.ru
BLACKBOX_URL=http://pass-stress-s1.sezam.yandex.net
PORTAL_ENVIRONMENT=stress
PORTAL_LOG_LEVEL=info
TZ=Europe/Moscow
PROCESS_COUNT=4
```

Domains:
api.stress.portal.ws.yandex.ru
