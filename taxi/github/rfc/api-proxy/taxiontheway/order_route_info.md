## Бизнесовая задача

Сервис, в котором можно спросить инфу по маршруту заказа и текущей позиции водителя на нем. 

## Архитектура

### API

Ручка `GET /v1/driver_pos`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
    "position": [
      76.948804,
      43.237497999999995
    ],
    "overdue": false,
}
```

Ручка `GET /v1/route_info`:

```json
{
    "order_id": "some_order_id",
    "driver_pos": [
      76.948804,
      43.237497999999995
    ],
}
```

```json
{
  "exact_pickup_point": [ ],
  "routeinfo": {
    "distance_left": 484,
    "time_left": 76,
    "max_time_left": 76,
    "positions": [
      {
        "info_key": "order_chain.parent_destination",
        "point": [
          60.588551,
          56.828491
        ],
        "type": "chain"
      }
    ],
}
```

Ручка `GET /v1/candidates_cars`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
    "freecars": {},
    "busycars": {}
}
```

### v1/driver_pos
Вообще, здесь просто поход в tracker/position с driver_id. Но так как вокруг есть логика,
которая проверяет текущий статус и время до подачи сравнивает с time_to_due_to_show_driver_position,
приходится выделять в отдельную ручку.
Подробнее логика здесь CanShowDriverPosition.

Нужно будет сходить в прок за driver_id и due.
####  Fallback
Можно просто не показывать.

### v1/route_info
Формирует инфу о маршруте. В driving водителя к пассажиру, в transporting - от текущей точки к точке назначения.
Основана на FillWithInfoOnRoute.
Возможно, стоит разделить на две ручки, одна для driving, другая для transporting.
positions появляется редко, вероятно при промежуточных точках, я сходу не понял, что значит active_chain_parent. И при комбо, но комбо уже нет.
Использует ручку smooth-routing трекера.
####  Fallback
Можно просто не показывать.

### v1/candidates_cars
Cходить в трекер за позициями найденных лукапом водителей. Это координаты на основании того, что лежит в кандидатах, так что вполне имеют отношение к маршруту.
freecars и busyсars ios не использует, спросил у дежурного ios:
"я на 99 процентов уверен что freecars не нужны
и на 100 процентов что busyсars не нужен"
Дежурный  Android скааал, что вообще не используются.
Водители вокруг есть из nearestdrivers, маршрут заказа есть в явном виде.
Кажется, эту ручку и эту часть ответа можно вообще не делать.
####  Fallback
можно просто не показывать.

### Технические детали и ограничения
1. Возможно, в этот сервис можно будет забрать всю информацию о маршруте поездки впоследствии. Но точки, которые шлет таксометр, обратабывает сервис core-engine.

