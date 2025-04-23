# Резолвер resolveCreateChat
## Описание

Создает чат

Обязательные параметры - `name` и `description`

Остальные необязательные:

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `channel` | string | Если хотим канал | - | - |
| `public` | boolean | Ставить true, чтобы появился inviteHash | - | - |
| `roles` | object | Можно добавить админов и другие роли | - | - |
| `members` | array | Список участников | - | - |
| `avatar_url` | string | Картинка для чата| -| - |
| `disable_members_updated_notifications` | boolean | Выключает системные сообщения о входе\выходе пользователей | - | - |

Описание параметров смотреть тут:
https://wiki.yandex-team.ru/messenger/api/registrymeta/#createchat

## Пример запроса (Postman)

URL запроса:
`<fapiUrl>/api/v2?name=resolveCreateChat`

Тело запроса

```
{
    "params": [{
        "name": "Тестовый чат",
        "description": "Тестовый чат",
        "roles": {"admin": ["7ff25b95-b770-45c1-bddb-36e0be38978e"]},
        "public": true
    }]
}
```

Создаст публичный чат с inviteHash
Админов в этом случае будет два - тот, кто чат создает, и тот, кто в запросе (в примере это бот)
Можно не указывать rolesб тогда будет один админ - создатель чата


## Пример успешного ответа

```
{
    "results": [
        {
            "handler": "resolveCreateChat",
            "result": {
                "status": "ok",
                "data": {
                    "restriction_status": "active",
                    "description": "Тестовый чат",
                    "roles": {
                        "admin": [
                            "7ff25b95-b770-45c1-bddb-36e0be38978e",
                            "5b872200-18bf-9fa1-6eb3-d27c6d2f46eb"
                        ]
                    },
                    "invite_hash": "6d6b1af3-2e09-4dab-98b1-6d2045078f0e",
                    "name": "Тестовый чат",
                    "version": 1613467778145320,
                    "chat_id": "0/24/c0947827-b458-4506-b44d-2652eb058d0e",
                    "members": [
                        "7ff25b95-b770-45c1-bddb-36e0be38978e",
                        "5b872200-18bf-9fa1-6eb3-d27c6d2f46eb"
                    ],
                    "create_timestamp": 1613467778.14532,
                    "permissions": {
                        "users": [
                            "7ff25b95-b770-45c1-bddb-36e0be38978e",
                            "5b872200-18bf-9fa1-6eb3-d27c6d2f46eb"
                        ]
                    }
                }
            }
        }
    ],
    "collections": {}
}```

Чтобы присоединиться к чату, нужно пройти по ссылке
`https://yandex.ru/chat/#/join/6d6b1af3-2e09-4dab-98b1-6d2045078f0e`
(id в конце строки - это invite_hash из ответа)
