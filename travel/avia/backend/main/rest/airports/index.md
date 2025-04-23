# Описание ручки
Ручка возвращает список аэропортов.

## Формат запроса:
```
GET /rest/airports?lang=<lang>&id=<id1>,<id2>
```

Если передан параметр id, происходит фильтрация по идентификаторам.

## Формат ответа:
```
GET http://<host>/rest/airports?id=9600370,9600215
{
    "status": "ok",
    "data": [
        {
            "timeZoneUtcOffset": 300,
            "stationType": {
                "prefix": "а\/п",
                "title": "аэропорт"
            },
            "code": "SVX",
            "urlTitle": "Koltsovo123",
            "title": "Кольцово123",
            "iataCode": "SVX",
            "longitude": 60.804833,
            "phraseFrom": "Кольцово123",
            "key": "s9600370",
            "popularTitle": "Кольцово123",
            "latitude": 56.750107,
            "timeZone": "Asia\/Yekaterinburg",
            "phraseIn": "Кольцово123",
            "settlement": {
                "country": {
                    "geoId": 225,
                    "title": "Россия"
                },
                "id": 54,
                "geoId": 54,
                "latitude": 56.838607,
                "longitude": 60.605514,
                "title": "Екатеринбург123"
            },
            "phraseTo": "Кольцово123",
            "id": 9600370
        },
        {
            "timeZoneUtcOffset": 180,
            "stationType": {
                "prefix": "а\/п",
                "title": "аэропорт"
            },
            "code": "VKO",
            "urlTitle": "Vnukovo",
            "title": "Внуково",
            "iataCode": "VKO",
            "longitude": 37.288233,
            "phraseFrom": "Внуково",
            "key": "s9600215",
            "popularTitle": "Внуково",
            "latitude": 55.605817,
            "timeZone": "Europe\/Moscow",
            "phraseIn": "Внуково",
            "settlement": {
                "country": {
                    "geoId": 225,
                    "title": "Россия"
                },
                "id": 213,
                "geoId": 213,
                "longitude": 37.619899,
                "latitude": 55.753676,
                "title": "Москва"
            },
            "phraseTo": "Внуково",
            "id": 9600215
        }
    ]
}
```
