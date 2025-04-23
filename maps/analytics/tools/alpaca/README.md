# alpaca

`alpaca` - это CLI-утилита для запуска и дебага метрик.

# Setup

1. [Счекаутить Аркадию](https://doc.yandex-team.ru/arc/setup/arc/install.html)
2. Собрать `alpaca`:

```
$ cd ~/arc/arcadia/maps/analytics/tools/alpaca
$ ya make
```

3. Установить симлинк, чтобы `alpaca` был доступен глобально

```
$ ln -snf ~/arc/arcadia/maps/analytics/tools/alpaca/alpaca  /usr/local/bin/alpaca
```

# Команды

## show

Выводит список метрик. Для печати всех полей (`key`, `values`) доступен флаг `-v`

Пример:

```
> alpaca metric-show --dataset basemap 

key: basemap
name: Метрики подложки
groups:
    key: basemap.events
    name: События
    metrics: 
        Дипъюз в карточке POI
        Дипъюз в карточке POI геопродукта
        Конверсия в дипъюз у POI
        Конверсия в дипъюз у POI геопродукта
        Открытие карточки POI
        Открытие карточки POI геопродукта

    key: basemap.sessions
    name: Сессии
    metrics: 
        Дипъюз в карточке POI
        Дипъюз в карточке POI геопродукта
        Конверсия в дипъюз у POI
        Конверсия в дипъюз у POI геопродукта
        Открытие карточки POI
        Открытие карточки POI геопродукта
```

Пример с флагом `-v`
```
> alpaca metric-show --dataset basemap -v

key: basemap
name: Метрики подложки
groups:
    key: basemap.events
    name: События
    metrics: 
        key: basemap.events.deep_use.poi.count
        name: Дипъюз в карточке POI
        values: 
            basemap.events.deep_use.poi.count$

        key: basemap.events.deep_use.geoproduct_poi.count
        name: Дипъюз в карточке POI геопродукта
        values: 
            basemap.events.deep_use.geoproduct_poi.count$

        key: basemap.events.deep_use.poi.cr
        name: Конверсия в дипъюз у POI
        values: 
            basemap.events.deep_use.poi.count$
            basemap.events.card_open.poi.count$

        key: basemap.events.deep_use.geoproduct_poi.cr
        name: Конверсия в дипъюз у POI геопродукта
        values: 
            basemap.events.deep_use.geoproduct_poi.count$
            basemap.events.card_open.geoproduct_poi.count$

        key: basemap.events.card_open.poi.count
        name: Открытие карточки POI
        values: 
            basemap.events.card_open.poi.count$

        key: basemap.events.card_open.geoproduct_poi.count
        name: Открытие карточки POI геопродукта
        values: 
            basemap.events.card_open.geoproduct_poi.count$
```

## debug

Запуск расчета метрик на `yt`

Пример:

```
> alpaca metric-debug --dataset basemap --service desktop-maps --date 2021-02-02
```

## local

Локальный запуск расчета метрик и вывод их в консоль

Пример:

```
> alpaca metric-local --dataset basemap --service desktop-maps --date 2020-02-02 -p dir/sample.json

metric_key                                       metric_name                             metric_value
-----------------------------------------------  ------------------------------------  --------------
basemap.events.card_open.poi.count               Открытие карточки POI                    1000
basemap.events.card_open.geoproduct_poi.count    Открытие карточки POI геопродукта          48
basemap.events.deep_use.poi.count                Дипъюз в карточке POI                     468
basemap.events.deep_use.geoproduct_poi.count     Дипъюз в карточке POI геопродукта          31
basemap.events.deep_use.poi.cr                   Конверсия в дипъюз у POI                    0.468
basemap.events.deep_use.geoproduct_poi.cr        Конверсия в дипъюз у POI геопродукта        0.645833
basemap.sessions.card_open.poi.count             Открытие карточки POI                     919
basemap.sessions.card_open.geoproduct_poi.count  Открытие карточки POI геопродукта          48
basemap.sessions.deep_use.poi.count              Дипъюз в карточке POI                     446
basemap.sessions.deep_use.geoproduct_poi.count   Дипъюз в карточке POI геопродукта          31
basemap.sessions.deep_use.poi.cr                 Конверсия в дипъюз у POI                    0.48531
basemap.sessions.deep_use.geoproduct_poi.cr      Конверсия в дипъюз у POI геопродукта        0.645833
basemap.users.card_open.poi.count                Открытие карточки POI                     905
basemap.users.card_open.geoproduct_poi.count     Открытие карточки POI геопродукта          47
basemap.users.deep_use.poi.count                 Дипъюз в карточке POI                     437
basemap.users.deep_use.geoproduct_poi.count      Дипъюз в карточке POI геопродукта          30
basemap.users.deep_use.poi.cr                    Конверсия в дипъюз у POI                    0.482873
basemap.users.deep_use.geoproduct_poi.cr         Конверсия в дипъюз у POI геопродукта        0.638298
```

# FAQ

## Как формируется путь до входной таблицы?

`//home/maps/analytics/datasets/{dataset_name}/{service}/{date}`

## Куда кладется таблица при запуске на YT?

`//home/maps/analytics/tmp/{$user_login}/datasets/{dataset_name}/{service}/{date}`

