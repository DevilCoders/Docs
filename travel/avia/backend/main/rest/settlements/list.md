# Описание ручки
Ручка возвращает все модели settlement из БД с возможностью фильтрации по id.

## Формат запроса:
```
GET /rest/settlements
```

## Формат ответа:
```
GET http://<host>/rest/settlements
{
    "status": "ok",
    "data": "data": [
        {
            "countryId": 225,
            "title": "Москва",
            "iata": "MOW",
            "phraseFrom": "Москва",
            "phraseIn": "Москва",
            "phraseTo": "Москва",
            "id": 213,
            "geoId": 213
        },
        ...
    ]
}
```

```
GET http://<host>/rest/settlements?id=213,214
{
    "status": "ok",
    "data": "data": [
        {
            "countryId": 225,
            "title": "Москва",
            "iata": "MOW",
            "phraseFrom": "Москва",
            "phraseIn": "Москва",
            "phraseTo": "Москва",
            "id": 213,
            "geoId": 213
        },
        {
            "countryId": 225,
            "title": "Долгопрудный",
            "iata": null,
            "phraseFrom": "Долгопрудный",
            "phraseIn": "Долгопрудный",
            "phraseTo": "Долгопрудный",
            "id": 214,
            "geoId": 214
        }
    ]
}
```
