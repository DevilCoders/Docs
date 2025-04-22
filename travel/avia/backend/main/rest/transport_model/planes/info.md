# Описание ручки
Ручка возвращает конкретную модель самолета
по коду из поля `www_transportmodel.code_en`.

## Формат запроса:
```
GET /rest/transport_model/planes/<code_en>
```

## Формат ответа:
```
GET http://<host>/rest/transport_model/planes/345
{
    "status": "ok",
    "data": {
        "code": "345",
        "code_en": "345",
        "is_cargo": false,
        "is_propeller_flight": false,
        "plane_body_type": "wire",
        "producer": "Airbus",
        "title": "Airbus A340-500",
        "title_en": "AIRBUS A340-600"
    }
}
```
