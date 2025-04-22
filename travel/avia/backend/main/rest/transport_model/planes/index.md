# Описание ручки
Ручка возвращает все модели самолетов из БД.

## Формат запроса:
```
GET /rest/transport_model/planes
```

## Формат ответа:
```
GET http://<host>/rest/transport_model/planes
{
    "status": "ok",
    "data": [
        {
            "code": "345",
            "code_en": "345",
            "is_cargo": false,
            "is_propeller_flight": false,
            "plane_body_type": "wire",
            "producer": "Airbus",
            "title": "Airbus A340-500",
            "title_en": "AIRBUS A340-600"
        },
        ...
    ]
}
```
