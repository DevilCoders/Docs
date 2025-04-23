# Резолвер addPostComplaint

## Описание

Принимает жалобу к посту

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `postId` | number | Айди поста | - |
| `text` | string | Текст жалобы, должен быть непустой для причины 1, иначе - пустая строка| "" |
| `reasonId` | number | 1 - "Другая" причина, 2 - "Спам и реклама" или 3 - "Оскорбление и нецензурные выражения" | - |

## Пример успешного ответа

```
{
    "results": [
        {
            "handler": "addPostComplaint",
            "result": {
                "result": false
            }
        }
    ],
    "collections": {}
}
```

## Пример неуспешного ответа

```
{
    "results": [
        {
            "handler": "addPostComplaint",
            "error": {
                "kind": "BadRequestError",
                "message": "Complaint with UID=94655204 for QUESTION=1828649 already exist"
            }
        }
    ],
    "collections": {}
}
```
Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addPostComplaint/v1/index.js)
- [Описание сущности `post` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/post/index.js)
