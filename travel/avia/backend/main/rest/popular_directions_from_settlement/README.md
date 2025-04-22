### PopularDirectionsFromSettlement

#### GET-Параметры:
```python
from_settlement_id = fields.Integer(required=True)
to_settlement_id = fields.Integer(required=True)
national_version = fields.String(required=True)
limit = fields.Integer(required=False, missing=5)
window_size = fields.Integer(required=False, missing=30)
```

#### Результат
На выходе возвращает `limit` (default=5) популярных направлений отсортированных по убыванию популярности в `national_version` из города отправления (`from_settlement_id`, за вычетом исходного пункта назначения (`to_settlement_id`).
Диапазон дат вылета: `[today, today + window_size]`
#####Формат ответа:
```json
[
    {
        "to_id": 239,
        "forward_date": "2020-04-11",
        "min_price": {
            "currency": "RUR",
            "value": 2999
        },
        "from_id": 54
    },
    {
        "to_id": 2,
        "forward_date": "2020-04-10",
        "min_price": {
            "currency": "RUR",
            "value": 2181
        },
        "from_id": 54
    }
]
```
