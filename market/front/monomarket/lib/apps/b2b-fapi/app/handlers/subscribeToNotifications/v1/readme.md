# Подписать пользователя на уведомления

Доступна по адресу `https://{host}/api/v1?name=subscribeToNotifications`

Проксирует запрос в Ксиву, ручка https://console.push.yandex-team.ru/#api-reference-subscribe-app
Кроме параметров (перечислены ниже), требует передать платформу в заголовке ```X-Platform``` (ios или android)

```typescript
type Params = {
    uuid: string; // идентификатор установки приложения
    token: string; // push токен
    appName: string; // название приложения в Ксиве
    deviceId?: string; // из мобильной метрики
};
```

```appName``` дополнительно валидируется и зависит от платформы, доступные значения [смотреть тут](https://github.yandex-team.ru/market/monomarket/blob/master/lib/apps/b2b-fapi/app/constants/applications.ts)

**Пример запроса**

```bash
curl --location --request POST 'https://{HOST}/api/v1?name=subscribeToNotifications' \
--header 'X-PLATFORM: ios' \
--header 'X-User-Authorization: OAuth {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
 "params": [{
     "appName": "ru.yandex.mobile.market.partner.inhouse",
     "token": "some token",
     "deviceId": "some deviceId",
     "uuid": "some uuid"
 }]
}'
```

**Ответ**
```json
{
    "results": [
        {
            "handler": "subscribeToNotifications",
            "result": "mob:uuid"
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
            "handler": "subscribeToNotifications",
            "error": {
                "kind": "ValidationError",
                "message": "Data has not pass validation",
                "details": {
                    "appName": {
                        "field": "appName",
                        "message": "App name has unexpectable value, maybe dependence attribute 'platform' is incorrect (null)",
                        "validator": "INCLUSION"
                    },
                    "platform": {
                        "field": "platform",
                        "message": "Platform can't be blank",
                        "validator": "PRESENCE"
                    }
                }
            }
        }
    ],
    "collections": {}
}
```