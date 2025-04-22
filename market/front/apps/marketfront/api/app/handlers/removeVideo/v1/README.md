# Резолвер removeVideo

## Описание

Резолвер передает в pers-author информацию об удалении видео, само видео из видеохостинга не удаляется.

В ответе приходит статус загрузки: успех или ошибка.

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `videoId` | string | Айди видео, которое нам вернул видеохостинг | - |

## Пример запроса

```text
curl --location --request POST 'https://<FAPI_URL>/api/v1/?name=removeVideo' \
--header 'Authorization: OAuth <Token>' \
--header 'Content-Type: application/json' \
--data-raw '{
    "params": [
        {
            "id": 62572,
            "videoId": "7cabadc8-7f02-4e45-b06d-0d86c0d90415"
        }
    ]
}'
```

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/removeVideo/v1/index.js)
- [Описание сущности `ugc-видео` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/ugcVideo/index.js)
