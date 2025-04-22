### NearbyAviaSettlements

#### GET-Параметры:
```python
settlement_id = fields.Integer(required=False)
geo_id = fields.Integer(required=False)
radius = fields.Integer(required=False, missing=200)
lang = fields.String(required=False, missing='ru', validate=validate.OneOf(LANG_ALLOWED))
```
- хотя бы один параметр из `settlement_id` и `geo_id` должен быть передан
- `radius` -  километры от заданной точки
- `lang` - язык для переводов

#### Результат
На выходе возвращает самолетные города (в которые можно прилететь)
в радиусе `radius` километров
от города заданного `settlement_id` или `geo_id`
в порядке возрастания удаленности.

##### Пример запроса
`/rest/nearby-avia-settlements?geo_id=&lang=ru&radius=250`

#####Формат ответа:
```json
[
    {
      "urlTitle": "Kaluga",
      "iata": null,
      "sirena": "КЛГ",
      "phraseIn": "Калуге",
      "id": 6,
      "distance": 160.2019617714,
      "countryId": 225,
      "title": "Калуга",
      "geoId": 6,
      "phraseFrom": "Калуги",
      "phraseTo": "Калугу"
    },
    {
      "urlTitle": "Markovo",
      "iata": null,
      "sirena": "МКО",
      "phraseIn": "Маркове",
      "id": 22215,
      "distance": 226.4677154331,
      "countryId": 225,
      "title": "Марково",
      "geoId": 144091,
      "phraseFrom": "Маркова",
      "phraseTo": "Марково"
    },
    {
      "urlTitle": "Ivanovo",
      "iata": "IWA",
      "sirena": "ИВВ",
      "phraseIn": "Иванове",
      "id": 5,
      "distance": 248.6689926958,
      "countryId": 225,
      "title": "Иваново",
      "geoId": 5,
      "phraseFrom": "Иванова",
      "phraseTo": "Иваново"
    }
]
```
