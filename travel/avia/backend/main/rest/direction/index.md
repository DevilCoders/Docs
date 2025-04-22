# Описание ручки
Ручка возвращает список популярных направлений.

## Формат запроса:
```
GET /rest/direction?national_version=ru
GET /rest/direction?national_version=ru&departure_settlement_id=1
GET /rest/direction?national_version=ru&arrival_settlement_id=2
GET /rest/direction?national_version=ru&departure_settlement_geo_id=1
GET /rest/direction?national_version=ru&arrival_settlement_geo_id=2
```

## Формат ответа:
```
GET http://<host>/rest/direction?national_version=ru&arrival_settlement_id=213&limit=2
{
    "status": "ok",
    "data": [
        {
            "connecting_flights": 7769059,
            "national_version": "ru",
            "popularity": 51946447,
            "arrival_settlement_id": 213,
            "departure_settlement_id": 146,
            "direct_flights": 8303626
        },
        {
            "connecting_flights": 6440205,
            "national_version": "ru",
            "popularity": 44387419,
            "arrival_settlement_id": 213,
            "departure_settlement_id": 239,
            "direct_flights": 6781199
        }
    ]
}
```
