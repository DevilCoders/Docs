# Описание ручки
Ручка возвращает список выбранных источников статусов для аэропортов.

## Формат запроса:
```
GET /rest/airport-tablo-source
GET /rest/airport-tablo-source?trusted=0
GET /rest/airport-tablo-source?trusted=1
```

## Формат ответа:
```
GET http://<host>/rest/airport-tablo-source
{
    "status": "ok",
    "data": [
        {
            "airport_id": 9859291,
            "source": "test1",
            "trusted": false
        },
        {
            "airport_id": 9600216,
            "source": "flight_stats+aurora",
            "trusted": true
        }
    ]
}
```
