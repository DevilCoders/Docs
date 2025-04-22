## Бизнесовая задача

Сервис получения данных по водителю, выполняющему заказ. Специально для taxiontheway по сути,
и подобных мест, где нужна инфа о водителе в контексте заказа.

## Архитектура

### API

Ручка `GET /v1/driver_info`:

```json
{
    "order_id": "some_order_id",
    "driver_id": "some_driver_id"
}
```

```json
{
    "color": "белый",
    "color_code": "FAFBFB",
    "feedback_badges": [    ],
    "model": "Hyundai Elantra",
    "name": "Мусаев Садам Батырович",
    "phone": "+79671503270,,9972",
    "photo_url": "",
    "pictures": {},
    "plates": "С805МС750",
    "profile_facts": [    ],
    "rating": "4.76",
    "short_name": "Садам",
    "status_title": "4.76 $RATING$",
    "tag": "47187297abf248817dff9d1a6575f43829b990a7d0abb496ce31130ddc4d7421",
    "yellow_car_number": false
}
```

Ручка `GET /v1/deaf_driver`:

```json
{
    "order_id": "some_order_id",
    "driver_id": "some_driver_id"
}
```

```json
{
    "button_modifiers": {},
    "force_destination": {},
}
```

Ручка `GET /v1/park_info`:

```json
{
    "order_id": "some_order_id",
    "park_id": "some_park_id"
}
```

```json
{
  "park": {
    "legal_address": "366904,село Брагуны,Дагестанская,74",
    "name": "Индивидуальный предприниматель Тавмурзаев Алибек Алиевич",
    "ogrn": "ОГРН: 318203600049790",
    "working_hours": "Часы работы: 9:00—18:00"
  },
  "partner": {
    "id": "400000110969",
    "legal_address": "366904,село Брагуны,Дагестанская,74",
    "long_name": "Индивидуальный предприниматель Тавмурзаев Алибек Алиевич",
    "name": "МИНУТКА",
    "ogrn": "ОГРН: 318203600049790",
    "phone": "+79265555614",
    "yamoney": false
  },
}
```

### v1/driver_info
Достает данные по водителю.
Все, кроме:
  позиции - ее мы спросим у сервиса маршрута заказа
  телефона - его мы спросим у сервиса с телефонами

Поговорил с Усковым. Можно использовать driver_profiles/v1/driver/profiles/retrieve для получения инфы по одному, но нужен кэш. Потому что кидать 3к рпс tow на внутренний сервис типа неправильно. Должно получиться что-то типа каскадной репликации: driver_profiles как мастер кеш, а отдельный сервис похода в driver_profiles или сама api-proxy как slave кэш. Можно делать LRU и ходить по одному, а можно забирать всех водителей и ходить за апдейтами.

Или можно сделать etag и не собирать данные каждый раз заново и тогда наверное можно будет обойтись без кешей.

Здесь же понадобится ходить в unique_drivers за рейтингом водителя. Когда дойдем до этого сервиса, нужно уточнить у Ускова состояние апи над этой коллекцией и как нам лучше решить задачу.
####  Fallback
Часть данных есть в order_proc.performer.

### v1/deaf_driver
Если водитель глухой, то возвращает нужные модификации в ответ.
####  Fallback
Можно просто не показывать.

### v1/park_info
Достает данные по парку.
Пусть будет пока так: мы можем использовать parks-replica/v1/parks/retrieve тоже наверное со своим кешом, но непонятно пока, это сервис над dbtaxi.parks или над dbparks.parks.
Над dbparks.parks новой стоит fleet-parks/v1/parks/contacts/retrieve и /v1/parks/list, но кажется, что нам этого недостаточно будет.
Поля, что нам нужны, можно посмотреть в protocol/lib/src/views/taxiontheway.cpp::BuildDataPark
#### Fallback
Часть данных есть в order_proc.performer.

### Технические детали и ограничения

