# Резолвер removePost

## Описание

Удаляет пост по его айди.
Для авторизованного пользователя

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `postId` | number | Айди поста | - |

## Пример успешного ответа

```
{
    "results": [
        {
            "handler": "removePost",
            "result": null
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
            "handler": "removePost",
            "error": {
                "kind": "BadRequestError",
                "message": "Can't remove already removed question"
            }
        }
    ],
    "collections": {}
}
```

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/removePost/v2/index.js)
- [Описание сущности `post` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/post/index.js)
