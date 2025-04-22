# Отписать пользователя на уведомления

Доступна по адресу `https://{host}/api/v1?name=unsubscribeFromNotifications`

Проксирует запрос в Ксиву, ручка https://console.push.yandex-team.ru/#api-reference-unsubscribe-app

```typescript
type Params = {
    uuid: string; // идентификатор установки приложения
};
```

**Пример запроса**

```bash
curl --location --request POST 'https://{HOST}/api/v1?name=unsubscribeFromNotifications' \
--header 'X-User-Authorization: OAuth {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
 "params": [{
     "uuid": "some uuid"
 }]
}'
```

**Ответ**
```json
{
    "results": [
        {
            "handler": "unsubscribeFromNotifications",
            "result": "OK"
        }
    ],
    "collections": {}
}
```

**Ошибки валидации**
```json
{
    "results": [
        {
            "handler": "unsubscribeFromNotifications",
            "error": {
                "kind": "ValidationError",
                "message": "Data has not pass validation",
                "details": {
                    "uuid": {
                        "field": "uuid",
                        "message": "Uuid can't be blank",
                        "validator": "PRESENCE"
                    }
                }
            }
        }
    ],
    "collections": {}
}
```