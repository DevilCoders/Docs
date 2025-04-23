# Резолвер removeChatMembers

## Описание

Удаляет всех участников чата

Обязательный параметр - chat_id

## Пример запроса в Postman

URL запроса:
`<fapiUrl>/api/v2?name=removeChatMembers`

Тело запроса

```
{
    "params": [{
        "chat_id": "0/24/c0947827-b458-4506-b44d-2652eb058d0e"
    }]
}
```

## Ответ

```
{
    "results": [
        {
            "handler": "removeChatMembers",
            "result": {
                "status": "ok",
            }
        }
    ],
    "collections": {}
}
