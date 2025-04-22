# Структура персональной цели

## Общая структура
```json
{
  "id": "уникальный идентификатор цели",
  "selection_id": "NY_2020_RIDE",
  
  "created": "дата создания цели",
  "updated": "дата обновления цели",
  
  "conditions": {},
  "bonus": {}
}
```

### Структура conditions

_5 поездок по эконому до 30 июля_
```json
{
  "conditions": {
    "type": "ride",
    
    "count": 5,
    "classes": ["econom"],
    
    "date_finish": "2019-07-30T12:00:00"
  }
}
```

_5 поездок по детскому тарифу ночью до 30 июля_
```json
{
  "conditions": {
    "type": "ride",
    
    "count": 5,
    "classes": ["child_tariff"],
    
    "time_start": "00:00",
    "time_end": "06:00",
    
    "date_finish": "2019-07-30T12:00:00"
  }
}
```

_5 поездок по эконому до 30 июля при оплате картой_
```json
{
  "conditions": {
    "type": "ride",
    
    "count": 5,
    "classes": ["econom"],
    "payment_types": ["card"], 
    
    "date_finish": "2019-07-30T12:00:00"
  }
}
```

_5 поездок по эконому до 30 июля при оплате картой в Москве_
```json
{
  "conditions": {
    "type": "ride",
    
    "count": 5,
    "classes": ["econom"],
    "payment_types": ["card"], 
    "source": {
      "zones": ["moscow"]
    },
    
    "date_finish": "2019-07-30T12:00:00"
  }
}
```

_5 поездок по эконому до 30 июля при оплате картой из Москвы в аэропорт_
```json
{
  "conditions": {
    "type": "ride",
    
    "count": 5,
    "classes": ["econom"],
    "payment_types": ["card"], 
    "source": {
      "zones": ["moscow"]
    },
    "destination": {
      "airport": true 
    },
    
    "date_finish": "2019-07-30T12:00:00"
  }
}
```

_5 поездок по эконому c 23 по 30 июля при наличии чаевых в заказе_
```json
{
  "conditions": {
    "type": "ride",
    
    "count": 5,
    "classes": ["econom"],
    
    "date_start": "2019-07-23T12:00:00",
    "date_finish": "2019-07-30T12:00:00",
    
    "with_tips": true
  }
}
```

_5 поездок по эконому c 23 по 30 июля при наличии фидбека в заказе_
```json
{
  "conditions": {
    "type": "ride",
    
    "count": 5,
    "classes": ["econom"],
    
    "date_start": "2019-07-23T12:00:00",
    "date_finish": "2019-07-30T12:00:00",
    
    "with_feedback": true
  }
}
```

_5 поездок по эконому или комфорту на следующие 7 дней с момента начисления_
```json
{
  "conditions": {
    "type": "ride",
    
    "count": 5,
    "classes": ["econom", "comfort"],
    
    "days_interval": 7
  }
}
```

_Купить Яндекс.Плюс до 30 июля_
```json
{
  "conditions": {
    "type": "ya_plus_buy",
    
    "date_finish": "2019-07-30T12:00:00"
  }
}
```

### Структура bonus

_Промокод_
За value, currency и percent надо ходить в сервис промокодов.
В качестве mvp предлагается зашить их тут и не ходить в сервис.
Также это значит что серию никто не должен редактировать.
```json
{
  "bonus": {
    "type": "promocode",
    "series": "bonus",
    
    "value": 400,
    "currency": "RUB",
    "percent": 10
  }
}
```

_Деньги на кошелек_
```json
{
  "bonus": {
    "type": "personal_wallet",
    
    "value": "100",
    "currency": "RUB"
  }
}
```
