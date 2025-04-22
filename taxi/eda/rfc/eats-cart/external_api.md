# API взаимодействия с внешними сервисами

## Получение информации о place по slug_name, shipping_type, position

В ответ приходит подмножество даннных из ответа ручки slug сервиса eats-catalog

Request

```json
{
    "slug": "slug",
    "shipping_type": "delivery",
    "position":[10,20],
    "delivery_time": "2020-01-01T00:00:00Z"
}
```

Response

```json
{
"place": {
    "name": "Корейское бистро Инсам (Афимолл)",
    "slug": "insam__bistro_afimoll_presnenskaya_naberezhnaya_2",
    "market": false,
    "available_payment_methods": [
      0,
      1,
      2,
      4
    ],
    "is_store": false,
    "business": "restaurant",
    "address": "Пресненская набережная, 2",
    "courier_type": "pedestrian",
    "courier_options": [],
    "available_shipping_types": [
        {
            "type": "pickup",
            "active": true
        },
        {
            "type": "delivery",
            "active": true
        }
    ]
  },
  "delivery_time": {
    "min":35,
    "max":45
    },
    "delivery_fee":79,
    "delivery_date_time":"25-02-2021 14:28",
    "delivery_date_time_iso":"2021-02-25T14:28:07+03:00",
    "requirements":{
        "sum_to_free_delivery":30,
        "sum_to_min_order":null,
        "next_delivery_threshold":"Закажите ещё на 30 ₽ для бесплатной доставки",
        "violated_constraints":[
        ]
    },
    "available_time_picker":[
        [
            "2021-02-25T15:30:00+03:00",
            "2021-02-25T16:00:00+03:00"
        ],
        [
            "2021-02-26T11:00:00+03:00",
            "2021-02-26T11:30:00+03:00",
            "2021-02-26T12:00:00+03:00"
        ]
    ],
    "country":{
        "id":35,
        "code":"RU",
        "currency":{
        "code":"RUB",
        "sign":"₽"
    }
    },
    "expenses_holding":null,
    "charges":[
        {
            "title":"Доставка Яндекс.Еды!",
            "type":"delivery",
            "cost":"79 $SIGN$$CURRENCY$",
            "payload":null
        }
    ],
    "surge": {
        "title": "title",
        "message": "message",
        "description": "description",
        "delivery_fee": 40
    }
}
```

## Получение информации о блюде по place_menu_item_id

POST /api/v2/menu/get_items

Request

```json
{
    "items":["item_1", "item_2",...]
}
```

Response

```json
{
    "place_slug": "koreiskiy_plov",
    "place_menu_items": [
        {
            "id": 142898127,
            "name": "Пибимпаб",
            "short_name": null,
            "description": "Рис с говядиной, яйцом и овощами (морковь, кабачки, огурцы, латук, ростки сои, нори) и говяжьим супом меок",
            "available": true,
            "in_stock": null,
            "price": 390,
            "decimal_price": "390.00",
            "promo_price": null,
            "options_groups": [
            {
                "id": 21876651,
                "name": "На выбор",
                "options": [
                {
                    "id": 176579156,
                    "name": "Острый",
                    "price": 0,
                    "decimal_price": "0.00",
                    "promo_price": null,
                    "multiplier": 1
                },
                {
                    "id": 176579161,
                    "name": "Средней остроты",
                    "price": 0,
                    "decimal_price": "0.00",
                    "promo_price": null,
                    "multiplier": 1
                },
                {
                    "id": 176579166,
                    "name": "Не острый",
                    "price": 0,
                    "decimal_price": "0.00",
                    "promo_price": null,
                    "multiplier": 1
                }
                ],
                "required": true,
                "min_selected": 1,
                "max_selected": 1
            }
            ],
            "picture": {
            "uri": "/images/1380157/c67f752739a45369aefd7b250d7cc685-{w}x{h}.jpg",
            "ratio": 1,
            "scale": "aspect_fill"
            },
            "weight": "400 г",
            "promo_types": [],
            "adult": false,
            "shipping_type": "all"
        }
    ]
}
```

## Получение корзины пользователя (ручка данного сервиса для использования в чекауте)

POST /api/v1/get_cart

Request

```json
{
 "eater_id": 1
}
```

Response

```json
{
    "items": [
        {
            "id": "some_id",
            "quantity": 4,
            "price": "20.10",
            "options": [
                {
                    "id": "option_id",
                    "price":"10.44",
                    "quantity": 1
                }
            ],
        }
    ],
    "promocode": {
        "code": "abc",
        "code_type": "type",
        "total_discount": "20.20",
        "percent": 20,
        "discount_limit": "20.20" 
    },
    "promos": [
        {
            "quantity": 5,
            "discount": 10,
            "TODO": "TODO"
        }
    ],
    "delivery_fee": "20.20",
    "delivery_date": "2021-03-10T11:11:11Z"
}
```
