## Расчет стоимости за проезд по платной дороге

### Концепция
В конце поездки определяем платные участки маршрута,
далее по известным данным о стоимости платных дорог определяем стоимость проезда для этих участков


### Реализация
1. Получаем информацию о заказе
2. Получаем маршрут заказа
3. Привязываем маршрут к графу для получения платности дороги
4. Получаем точки въезда/выезда для платных дорог
5. По точкам въезда и выезда с платного участка определяем стоимость для пользователя


### 1. Получаем информацию о заказе
Запрос в [order-core](https://wiki.yandex-team.ru/taxi/backend/architecture/taxi-order-core/)

Endpoint:  [/v1/tc/order-fields](https://github.yandex-team.ru/taxi/uservices/blob/develop/services/order-core/docs/yaml/api/api.yaml#L113)

```
Пример запроса:

{
   "order_id": "b2fb46da4be363e0b46773ca6277c33c",
   "fields": [
      "order.performer.real_clid",               # db_id
      "order.performer.uuid",                    # driver_id
      "order_info.statistics.status_updates.t",  # статус заказа
      "order_info.statistics.status_updates.c",  # время установки статуса
   ],
   "require_latest": True,
   "search_archive": False
}
```

В `order_info.statistics.status_updates` находим время установки статусов
- "transporting" - поездка началась
- "complete"     - поездка завершилась


### 2. Получаем маршрут заказа
Данные о маршруте забираем из [geotracks](https://wiki.yandex-team.ru/taxi/backend/architecture/geotracks/)

Endpoint: [/gps-storage/get](https://github.yandex-team.ru/taxi/backend-cpp/blob/master/geotracks/docs/yaml/gps-storage-get.yaml#L11)

```
Пример запроса:

/gps-storage/get?
     db_id=a3608f8f7ee84e0b9c21862beef7e48d      # order.performer.real_clid
    &driver_id=84bf334913f14ea194867d8d8e51cd0b  # order.performer.uuid
    &from=1590646599                             # timestamp установки статуса заказа в "transporting"
    &to=1590647735                               # время установки статуса заказа в "complete"
    &verbose=true

Пример ответа:
{
   "track":[
      {
         "bearing":0.0,
         "cost":0.0,
         "distance":0.0,
         "end":false,
         "order_status":0,
         "point":[
            37.607269287109375,
            55.743423461914062
         ],
         "speed":0.0,
         "status":2,
         "timestamp":1590646575
      },
      ...
      {
         "bearing":0.0,
         "cost":0.0,
         "distance":0.0,
         "end":true,
         "order_status":0,
         "point":[
            37.603958129882812,
            55.774307250976562
         ],
         "speed":0.0,
         "status":2,
         "timestamp":1590647745
      }
   ]
}
```


### 3. Привязываем маршрут к графу для получения платности дороги
Запрос в [yaga-adjust](https://wiki.yandex-team.ru/taxi/backend/graph/services/yaga-adjust/)

Endpoint:  [/adjust/track](https://github.yandex-team.ru/taxi/uservices/blob/develop/schemas/services/yaga-adjust/api/adjust-track.yaml#L12)

```
Пример запроса:

/gps-storage/get?
     db_id=a3608f8f7ee84e0b9c21862beef7e48d     
    &driver_id=84bf334913f14ea194867d8d8e51cd0b
    &from=1590646599                             # время установки заказа в статус "transporting"
    &to=1590647735                               # время установки заказа в статус "complete"
    &verbose=true
    
/adjust/track?       
     algorithm=auto
    &timeout=1000

{
    "track": [
        {
            "direction":0,
            "lat":55.744929999999997,
            "lon":37.613912999999997,
            "timestamp":1592213006
        }, 
        ...
        {
            "direction":0,
            "lat":55.745384999999999,
            "lon":37.613546999999997,
            "timestamp": 1592213011
        }
    ],
    'interpolate': True
}

Пример ответа:
{
    "positions": [
        {
            "lat":55.744929951057709,
            "lon":37.613912808017818,
            "timestamp":1592213006,
            "direction":335.0,
            "is_toll":false,
            "is_null":false
        },
        ...
        {
            "lat":55.74538492876315,
            "lon":37.61354672055817,
            "timestamp":1592213011,
            "direction":335.0,
            "is_toll":true,
            "is_null":false
        }
    ]
}
```

### 4. Получаем точки въезда/выезда для платных дорог

Проходимся по списку "positions" из ответа yaga-adjust, формируя список [(точка_въезда, точка выезда), ...], ориентируясь на параметр "is_toll": true/false.

### 5. По точкам въезда и выезда с платного участка определяем стоимость для пользователя

Необходимо сопоставить точки въезда/выезда для платных дорог с пунктами въезда/выезда из конфига.

#### Подробнее про конфиг:

Конфиг содержит информацию о стоимости проезда по платным участкам.

Параметры, от которых зависит цена платного участка:
- точка въезда/выезда
- день недели
- время проезда
- класс транспортного средства (легковая/грузовая машина)

Подробнее про тарифы:
- ЗСД: https://nch-spb.com/tariffs/cash/
- М11: https://15-58m11.ru/trip/grid/


Дополнительно:

Скрипт, который реализует логику пунктов 1-3 https://github.yandex-team.ru/yuldash/snippets/blob/master/toll_roads.py

