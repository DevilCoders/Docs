# Резолвер addReviewComplain

## Описание

Принимает жалобу к товарному или магазинному отзыву

Может принять жалобу от незалогина

Может принять жалобу на несуществующий отзыв (бекенд не проверяет это)

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `entityId` | number | Айди отзыва | - |
| `text` | string | Текст жалобы, должен быть непустой для причины 1, иначе - пустая строка| "" |
| `reasonId` | number | 1 - "Другая" причина, 2 - "Спам и реклама", 3 - "Оскорбление и нецензурные выражения" или 16 - "Информация не соответствует действительности" | - |

## Пример успешного ответа

```
{
    "results": [
        {
            "handler": "addReviewComplaint",
            "result": true
        }
    ],
    "collections": {}
}
```

## Пример неуспешного ответа (неизвестный id жалобы)

```
{
    "results": [
        {
            "handler": "addReviewComplaint",
            "error": {
                "kind": "ValidationParamsHandlerError",
                "message": "10 is not included in the list"
            }
        }
    ],
    "collections": {}
}
```
Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/addReviewComplaint/v1/index.js)
