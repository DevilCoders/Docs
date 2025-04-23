# Описание ручки
Ручка возвращает информацию об отзывах на рейс.

## Формат запроса:
```
GET /rest/airlines/<airline_id>/flights/<flight_number>/reviews
```

## Формат ответа:
```
GET http://<host>/rest/airlines/94/flights/473/reviews
{
    "status": "ok",
    "data": {
        "total": 1,
        "airline_total": 29
    }
}
```
