# Desktop Notifications

### Как это все работает

Есть объект нотификашки разных типов, вида:

```javascript

   {
    "cards": [
      {
        "expanded": 0,
        "name": "domik",
        "order": 0
      },
      {
        "actions": {
          "ban": "https://www-v82d4.wdevx.yandex.ru/portal/set/any/?sk=u22bd505a5d9c88850a9df4cf2c072002&dntf=dstr:me:*",
          "close": "https://www-v82d4.wdevx.yandex.ru/portal/set/any/?sk=u22bd505a5d9c88850a9df4cf2c072002&dntf=dstr:me:5c25"
        },
        "data": {
          "counter": "metro",
          "domain": "ru",
          "from": "2017-12-22 17:00",
          "geos": "225",
          "icon": "metro_green",
          "lang": "all",
          "popup_flag": "1",
          "text": "23–24 декабря",
          "till": "2018-12-25 01:00",
          "title": "Закрытие станций метро Замоскворецкой линии",
          "type": "metro"
        },
        "expanded": 0,
        "name": "disaster",
        "order": 1
      },
      {
        "actions": {
          "ban": "https://www-v82d4.wdevx.yandex.ru/portal/set/any/?sk=u22bd505a5d9c88850a9df4cf2c072002&dntf=rout:*:",
          "close": "https://www-v82d4.wdevx.yandex.ru/portal/set/any/?sk=u22bd505a5d9c88850a9df4cf2c072002&dntf=rout::4d9c"
        },
        "data": {
          "direction": "reverse",
          "direction_by_distance": "reverse",
          "finish": {
            "address_line": "Россия, Москва, улица Льва Толстого, 16",
            "address_line_short": "улица Льва Толстого, 16",
            "data_key": "work",
            "latitude": 55.733842,
            "longitude": 37.588144,
            "tags": {
              "_w-_traffic-1-finish": 1
            },
            "title": "Работа"
          },
          "setup_direction": "direct",
          "start": {
            "address_line": "Москва, проспект 60-летия Октября, 3к3",
            "address_line_short": "проспект 60-летия Октября, 3к3",
            "data_key": "home",
            "latitude": 55.70562,
            "longitude": 37.582574,
            "tags": {
              "_w-_traffic-1-start": 1
            },
            "title": "Дом"
          },
          "storage": "personal"
        },
        "expanded": 0,
        "name": "route",
        "order": 2
      },
      {
        "actions": {
          "ban": "https://www-v82d4.wdevx.yandex.ru/portal/set/any/?sk=u22bd505a5d9c88850a9df4cf2c072002&dntf=zen:*:",
          "close": "https://www-v82d4.wdevx.yandex.ru/portal/set/any/?sk=u22bd505a5d9c88850a9df4cf2c072002&dntf=zen::"
        },
        "expanded": 0,
        "name": "zen",
        "order": 3
      }
    ],
    "processed": 1,
    "show": 1
  }
```

По каждой нотификашке имеется возможность забанить  ее, то есть убрать показ только еэтой карточкие или ее тип/субтип совсем.
За это отвечают объекты в куке YP или DataSync вида


```
[
    {
      "mark": "*",
      "subtype": "fa",
      "time": 1523029982,
      "type": "dstr"
    },
    {
      "mark": "*",
      "subtype": "me",
      "time": 1523029982,
      "type": "dstr"
    },
    {
      "mark": "*",
      "subtype": "tr",
      "time": 1523029982,
      "type": "dstr"
    }
  ]
```

Type, SubType понятно за что отвечают, а вот поле Mark - это поле, которое отвечает за то, что конкретно в рамках данного типа/субтипа блокируем. Если там хеш(набор сиволов), то мы блокируем только конкретную карточку, а если там звездочка в subtype или mark, то мы блокируем тип или субтип всех карточек соответственно. Тюн работает только со звездочками.
