### Ручка для сообщения решения о модерации рассылки

```
POST /api/0/<account-slug>/campaign/<campaign-slug>/moderation
```

Ручка требует скоуп `moderate:write`. Так же в ручку отдельно разрешено ходить Янгу со своим твм-тикетом для сообщения вердиктов модерации. Установка статуса модерации идемпотентна: можно при необходимости повторить запрос с одинаковым вердиктом (однако запрос с противоположным вердиктом будет считаться ошибкой).

#### Параметры
Параметры передаются в теле запроса в JSON.

- `accept`: `true` или `false` - принять или отклонить кампанию

#### Примеры
```bash
curl -X POST -H "content-type:application/json" \
    -u ce3ee6e2bdf3484f9b02b080694af289: \
    -d '{"accept": true}' \
    https://test.sender.yandex-team.ru/api/0/Yandex.Mail/campaign/4938H6K3-BU7/moderation
```

Ответ Ок:
```json
{"result":  {"status": "OK"}}
```

Ответ 400 Bad Request:
```json
{"result": {"status": "ERROR", "message": "Wrong campaign state"}}
```
