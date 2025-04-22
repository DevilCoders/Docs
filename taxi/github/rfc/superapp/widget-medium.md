### Описание

Endpoint для отображения виджета среднего размера на клиентах. Показываем турбокнопки /кирпичи / шорткаты точки Б.

### Клиентское API

Ручка `4.0/mlutp/v1/widget/medium`.

Request:
```json5
{
  "position": [
    37.46846738204889,
    55.73701221416811
  ],
  "typed_experiments": {
    "items": []
  },
  "state": {
    "accuracy": 16,
    "known_orders": [],
    "multiclass_options": {},
    "selected_class": "econom"
  }
}
```

Response:
```json5
{
    "widget": {
        "header": {
            "title": "Такси",
            "subtitle": "Указать адрес...",
            "icon_tag": "superapp_colored_brick_taxi:9b8265",
            "deeplink": "yandextaxi://route?expandingState=expanded"
        },
        "services": [
            {
                "service": "grocery",
                "title": "Лавка",
                "icon_tag": "shortcuts_buttons_grocery_disabled",
                "deeplink": "yandextaxi://external?service=grocery"
            },
            {
                "service": "delivery",
                "title": "Доставка",
                "icon_tag": "shortcuts_buttons_delivery",
                "deeplink": "yandextaxi://route?tariffClass=express"
            },
            {
                "service": "city",
                "title": "Город",
                "icon_tag": "city_icon_tag",
                "deeplink": "yandextaxi://city-mode"
            }
        ],
        "shortcuts": [
            {
                "title": "Домой",
                "subtitle": "Льва Толстова, 16",
                "icon_tag": "home",
                "deeplink": "yandextaxi://route?end-lat=55.733974&end-lon=37.587093"
            },
            {
                "title": "На работу",
                "subtitle": "МФК Око",
                "icon_tag": "work",
                "deeplink": "yandextaxi://route?end-lat=55.750028&end-lon=37.534406"
            }
        ]
    },
    "typed_experiments": {
        "items": [],
        "version": 965755
    }
}
```
