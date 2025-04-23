## Интеграция с Q
[Докементация](https://botplatform.yandex.net/docs/)

## Заведение бота в alpha-среде
```
curl -H "Authorization: OAuthTeam <TOKEN>" https://botplatform.alpha.yandex.net/team/register/
```
Внимание! важно добавлять "/" на конце урла!
В ответ должен прийти такой json:
```
{
    "bot": {
        "guid":"4fb53588-93f6-4a5b-b494-396790c2c886",
        "nickname":"robot-hroom"
    },
    "registered":true,
    "ok":1
}
```


## Урл для общения с ботом, который был создан в alpha-среде
```
https://messenger.alpha.yandex-team.ru
```


## Установка webhook_url
```
curl -H "Authorization: OAuthTeam <TOKEN>" \
    -d '{"webhook_url": <WEBHOOK_URL>}' \
    -H "Content-Type: application/json" \
    -X POST \
    https://botplatform.alpha.yandex.net/team/update/
```
В ответ должен прийти такой json:
```
{
    "uid":"1120000000165712",
    "guid":"4fb53588-93f6-4a5b-b494-396790c2c886",
    "nickname":"robot-hroom",
    "display_name":"synced team bot",
    "description":null,
    "is_alice_skill":false,
    "webhook_url":<WEBHOOK_URL>,
    "webhook_tvm_id":null,
    "type":"telegram_like",
    "website":null,
    "average_response_time":null,
    "settings":{},
    "service_id":4,
    "location":null,
    "sprav_org_id":null,
    "robot_info":{}
}
```
По этому урлу бот должен будет отправлять запросы на каждое входящее сообщение.
Для того, чтобы Q мог слать сообе