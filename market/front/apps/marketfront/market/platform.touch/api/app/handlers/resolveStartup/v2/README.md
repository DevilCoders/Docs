# Резолвер resolveStartup

## Описание

Подписывает приложение на уведомления, отправлет silent-пуш с первым токеном авторизации

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `appName`* | string | Идентификатор приложения | - | - |
| `pushToken`* | string | В зависимости от платформы передайте device token (apns) или registration id (fcm) | - | - |

\* - обязательный параметр

## Пример запроса
```sh
curl --request POST \
  --url '<FAPI host>/api/v2?=&name=resolveStartup' \
  --header 'content-type: application/json' \
  --data '{
	"params": [{
        "appName": "ru.yandex.market",
        "pushToken": "<PUSH_TOKEN>",
    }]
}'
```

## Пример ответа
```json
{
    "results": [
        {
            "handler": "resolveStartup",
            "result": "OK"
        }
    ],
    "collections": {
        "response": [
            {
                "code": 200,
                "body": {
                    "message_id": "0:1594889717654873%4f755b90f9fd7ecd"
                },
                "id": "mob:83c58a0c00a54791b9f4c7d7a6fa307b"
            }
        ]
    }
}
```

## Полезные ссылки
- [Описание сущности `region` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/region/index.js)
