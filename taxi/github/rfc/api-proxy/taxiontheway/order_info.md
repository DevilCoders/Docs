## Бизнесовая задача

Сервис, в котором можно спросить инфу по заказу. Не такая критичная информация, как в order-core и с возможностью добавить какую-то логику. К примеру, order-core просто вернет цену из прока, а ручка cost этого сервиса сможет еще скидки/промокоды/платную подачу посчитать.
То есть почти как обычный микросервис над базой, только эта база order_proc.

## Архитектура

### API

Ручка `GET /v1/сost`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
   "cost_message": "От 100 $SIGN$$CURRENCY$",
   "cost_message": 100,
   "cost_message_details": {},
   "final_cost": 100,
   "coupon": {}, // просто забирает из прока, нет смысла отделять 
   "discount": {}, // почти то же самое, что coupon, странно
   "paid_supply_discount": {}// скидка, если нашелся водитель поближе, только на основании прока
}
```

Ручка `GET /v1/changes`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
    "allowed_changes": [ ],
    "payment_changes": [ ],
    "pending_changes": [ ],
    "user_ready": false
}
```

Ручка `GET /v1/route_sharing`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
    "route_sharing_url": "https://taxi.yandex.ru/route/c35dd2632adebdd917428f7036a0882a"
}
```

Ручка `GET /v1/extra_contact_phone`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
    "extra_contact_phone": "+79991234567"
}
```

Ручка `GET /v1/granted_promotions`:

```json
{
    "order_id": "some_order_id"
}
```

```json
{
  "higher_class_dialog": {
    "class_after_upgrade": "comfortplus",
    "image": "class_comfortplus_car",
    "text": "Free upgrade. Thanks for riding with us!",
    "title": "Comfort+ is on the way"
  },
  "granted_promotions": []
}
```

### v1/cost
Вся инфа по стоимости заказа, что нужно вернуть в totw. Взять данные из прока, посчитать скидки, промокоды итд. Умеет вернуть собственно примененные скидки и купоны, и скидку платной подачи, если нашелся водитель поближе.
Тут даже есть hourly_rental_price_info. Калькулятора нет.
Сейчас планируется сделать простой копипаст из backend-cpp, после появления прайсинга - ходить в него.
####  Fallback
Используем цены из order-core.

### v1/changes
Изменения в заказе, которые можно внести и которые уже внесены.
####  Fallback
Можно просто не показывать.

### v1/route_sharing
Просто взять из прока route_sharing_url
####  Fallback
можно просто не показывать.

### v1/extra_contact_phone
Если в проке есть extra_contact_phone, то сходить в user-api за номером телефона и вернуть его. Кажется, никакого софтсвитча там нет.
####  Fallback
можно просто не показывать.

### v1/granted_promotions
Заполняет поля order_granted_promotions и higher_class_dialog на основании granted_promotions из прока.

Про promotions долгая история:
1. в backend-py2 есть promotions_manager.py, который на изменения статуса на assigned и complete вызывыет некоторый набор хэндлеров. 
  - При этом фактически работают только обработчики на assigned
  - Есть 4 хэндлера:
    - промо higher_class_car про повышенный класс
    - промо genesis с Hyundai Genesis
    - промо EA2016 с Battlefield 1 
    - промо Elki5 про Ёлки, собственно
  - Актуален только хэндлер про повышенный класс
2. Сформированные промоакции пишутся в order_proc.granted_promotions
3. taxiontheway смотрит в это поле и
  - отдельно для промо higher_class_car формирует поле higher_class_dialog
  - все остальные промо складывает в granted_promotions
4. Поле granted_promotions в ответе присутствует всегда
5. Я не нашел в проде записей в order_proc, где в granted_promotions лежит не higher_class_car

В итоге получается, что поле granted_promotions в ответе всегда пустое. И вообще весь механизм на основе order_proc.granted_promotions существует только для higher_class_car.
Мне кажется, его можно попробовать просто пересадить на новый сервис фулскринов - promotions.

Если мы не будем этого делать, то остается только перенести логику про higher_class_car в эту ручку.
####  Fallback
можно просто не показывать.

### Технические детали и ограничения
1. Все ручки readonly, мы ничего не пишем в прок
2. Используем для получения данных ручку сервиса order-core

