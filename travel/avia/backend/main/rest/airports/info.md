# Описание ручки
Ручка возвращает информацию по аэропорту по идентификатору.

## Формат запроса:
```
GET /rest/airports/<station_id>?lang=<lang>
```

## Формат ответа:
```
GET http://<host>/rest/airports/9600370?lang=ru
{
    "status": "ok",
    "data": {
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
            "latitude": 56.838607,
            "country": {
                "geoId": 225,
                "title": "Россия"
            },
            "id": 54,
            "geoId": 54,
            "longitude": 60.605514,
            "title": "Екатеринбург123"
        },
        "phraseTo": "Кольцово123",
        "id": 9600370
    }
}
```
