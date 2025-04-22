Ручка `/landing/route/{fromId}/{toId}/{nationalVersion}`
----

### Формат запроса
`/landing/route/?fromId=<fromId>&toId=<toId>/nationalVersion=<nationalVersion>&fields=field1,field2`

- `fromId`, `toId` - Идентификаторы городов (`uint32`)
- `nationalVersion` - Национальная версия (`string`)
- `fields` - список необходимых полей (`comma-separated strings`):
    - `alternativeRoutesPrices`
    - `medianPrices`
    - `popularMonth`
    - `returnTicketPrice`
    - `routeInfo`
    - `topAirlines`

### Формат ответа
Запрос: `/landing/route/&fromId=213&toId=2&nationalVersion=ru&fields=popularMonth,returnTicketPrice`

- если `fields` не передан -- возвращает данные для всех полей
- если нет данных ни по одному полю, возвращает `HTTP 404`:
```json
{
  "error": {
    "Message": "not found"
  }
}
```
- формат ответа для всех полей:
```json
{
  "result": {
    "fromId": 213,
    "toId": 2,
    "popularMonth": {
      "year": 2020,
      "month": 10,
      "price": 999,
      "currency": "RUR",
      "date": "2020-10-12"
    },
    "returnTicketPrice": {
      "price": 1499,
      "currency": "RUR",
      "date": "2020-09-08"
    },
    "alternativeRoutesPrices": [
      {
        "alternativeToId": 28229,
        "price": 7836,
        "currency": "RUR",
        "date": "2020-09-10"
      }
    ],
    "medianPrices": {
      "month": 3,
      "year": 2020,
      "monthMedianPrice": 2405,
      "yearMedianPrice": 3279,
      "currency": "RUR"
    },
    "routeInfo": {
      "distance": 634,
      "duration": 125,
      "fromAirports": [
        9850865,
        9600213,
        9600215,
        9600216
      ],
      "toAirports": [
        9600366
      ]
    },
    "topAirlines": [
      29,
      9144,
      8565,
      30,
      26,
      23,
      2543,
      1364
    ]
  }
}
```
