# Описание ручки
Ручка возвращает информацию по COVID-19 ограничениям для стран.

## Формат запроса:
```
GET /rest/country-restrictions(/<country_id>)?
```

## Формат ответа:
### С указанием страны
```
GET http://<host>/rest/country-restrictions/21326
{
  "status": "ok",
  "data": {
    "passes": "",
    "fullText": "",
    "countryId": 21326,
    "mask": "",
    "selfIsolation": "",
    "isClosed": false,
    "gloves": "",
    "closedText": "",
    "borders": "Ограничения при пересечении границы",
    "untilDate": ""
  }
}
```

России нет в списке
```
GET http://<host>/rest/country-restrictions/225
{
  "status": "ok",
  "data": null
}
```

### Без указания страны. Получить все ограничения
```
GET http://<host>/rest/country-restrictions
{
  "status": "ok",
  "data": [
    {
      "passes": "",
      "fullText": "",
      "countryId": 84,
      "mask": "",
      "selfIsolation": "",
      "isClosed": false,
      "gloves": "",
      "closedText": "",
      "borders": "Ограничения при пересечении границы",
      "untilDate": ""
    },
    
    {...},

    {
      "passes": "",
      "fullText": "",
      "countryId": 20989,
      "mask": "",
      "selfIsolation": "",
      "isClosed": false,
      "gloves": "",
      "closedText": "",
      "borders": "Ограничения при пересечении границы",
      "untilDate": ""
    }
  ]
}
```
