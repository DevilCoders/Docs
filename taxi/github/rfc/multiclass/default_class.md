### Описание
Необходимо добавить возможность сделать мультикласс дефолтно выбранным тарифом

### Проблемы
нельзя делать это через стандартный механизм дефолтов, так как 
1) мультикласс не тариф в классическом понимании этого слова (у него нет своего типа, как например у комфорта business)
2) мультиклассу необходим как минимум один запрос в routestats, чтобы понять какие классы доступны, какая максимальная цена у выбранных классов

### Решение
#### Клиентский протокол
сохранять в personalstate не только selected_classes, но и факт выбранности мультикласса
```(json)
{
...
"multiclass_options": {
    "class": [
      "econom",
      "business"
    ],
    "selected": false
  },
...
}
```

Тогда отображениие мультикласса будет состоять из следующих этапов:
1) делаются блокиирующие запрос в zoneinfo и personalstate
2) отображениие мультикласса в селекторе тарифов и его дефолтности
3) если клиент нажимает на мультикласс до ответа routestats - показывать тарифы из локального кеша на стороне клиентов

**локальный кеш:**
Клиенты кэшируют список классов мультикласса из последнего запроса в роутстатс в этой же зоне:
- если мультикласс был недоступен - спиисок очищается
- если мультикласс доступен - сохраняются все классы, которые доступны в мультиклассе
Если классов в кеше нет — не показывать мультикласс до ответа роутстатс

Также в zoneinfo в поле multiclass
```
"multiclass": {
"type": "multiclass",
"can_be_default": true,
"details": {
  "description": "Будем искать машину в нескольких тарифах сразу. Приедет ближайшая.",
  "order_button": {
    "text": "Выберите минимум два тарифа"
  },
  "search_screen": {
    "subtitle": "в нескольких тарифах",
    "title": "Поиск"
  }
},
"multiclass_popup": {
  "show_conditions": [
    {
      "count": 3,
      "metric": "tariff_switch",
      "period_seconds": 8
    }
  ],
  "show_count": 3,
  "text": "Самый\\nбыстрый"
},
"name": "Самый быстрый",
"selection_rules": {
  "min_selected_count": {
    "text": "Выберите минимум два тарифа",
    "value": 2
  }
},
"selector": {
  "icon": {
    "size_hint": 320,
    "url": "https://tc.mobile.yandex.net/static/images/40230/8d445b51ebc84eca9b3e1a5dcbb17313",
    "url_parts": {
      "key": "TC",
      "path": "/static/images/40230/8d445b51ebc84eca9b3e1a5dcbb17313"
    }
  }
}
}
```

