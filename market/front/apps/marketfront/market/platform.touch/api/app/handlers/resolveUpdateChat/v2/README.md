# Резолвер resolveUpdateChat

## Описание

Позволяет поменять настройки чата

Обязательный параметр - chat_id

Остальные:

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `description` | string | Новое описание | - | - |
| `name` | string | Новое название | - | - |
| `avatar_url` | string | Новая аватарка | -| - |
| `public` | boolean | Вкл/выкл публичность чата | - | - |
| `disable_members_updated_notifications` | boolean |  | - | - |

Описание параметров смотреть тут:
https://wiki.yandex-team.ru/messenger/api/registrymeta/#updatechat

## Пример запроса в Postman

URL запроса:
`<fapiUrl>/api/v2?name=removeChatMembers`

Тело запроса

```
{
    "params": [{
        "chat_id": "0/24/c0947827-b458-4506-b44d-2652eb058d0e",
        "public": true
    }]
}
```

Такой запрос сделает чат публичным и добавит inviteHash в ответе
