# Прогнозатор стоимости доставки (CostForecaster)
Тестировалось на `Python 3.6.8`

#### Принцип работы
1. По умолчанию из БД `market-orders-dict` выгружаются все заказы за вчера.
2. По каждому заказу прогнозируются косты на доставку, страховка, другие косты и возврат.
3. База заказов со спрогнозированными костами за услуги и текушим статусом записывается в папку с прогнозатором.

В случае, когда для заказа за вчера не известен конечный статус, при следующем запуске проверяется, 
произошло ли изменение его статуса на `RETURN` и если произошло, заказ выгружается для уточнения поля `return_cost`.

У заказа могут быть нули по всем полям, что означает, что для данного заказа не было найдено 
соответствующее правило в тарифах на доставку. Такие заказы должны логироваться.

Так как на данный момент запись таблицы на YT не реализована результатом работы скрипта является 
запись таблицы с предсказаниями в папку `files`.

#### Настройка
1. По пути `configs/db.py` в переменную `TOKEN` требуется записать токен для доступа к YQL.
2. (Опционально) По пути `configs/queries.py` можно изменять составляющие запроса к БД.

#### Пример запуска
```bash
python run.py
```

# Sandbox
## Собрать и загрузить ресурс руками
1. ```ya package pkg.json```
2. ```ya upload --type=MARKET_COST_FORECASTER_APP {tar_gz_name}```
## Собрать и загрузить ресурс таской в sandbox
Склонировать и запустить [sandbox](https://sandbox.yandex-team.ru/task/543571435/view).
## Запустить задачу RUN_COST_FORECASTER
Склонировать и запустить [sandbox](https://sandbox.yandex-team.ru/tasks?type=RUN_COST_FORECASTER&limit=10).

## Sheduler
Настроен шедулер на запуск 1 раз в сутки, в 8:00.
Используется последняя версия ресурса.

## Links
 * [Resource MARKET_COST_FORECASTER_APP](https://sandbox.yandex-team.ru/resources?type=MARKET_COST_FORECASTER_APP&limit=10)
 * [Task YA_PACKAGE для сборки MARKET_COST_FORECASTER_APP](https://sandbox.yandex-team.ru/task/543571435/view)
 * [Task RUN_COST_FORECASTER](https://sandbox.yandex-team.ru/tasks?type=RUN_COST_FORECASTER&limit=10)
 * [sheduler](https://sandbox.yandex-team.ru/scheduler/18352/view)

# Результаты работы
 * [Все таблицы на hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/opsmoda/cost_forecaster&)
 * [Последняя выгрузка](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/opsmoda/cost_forecaster/latest&offsetMode=row)
