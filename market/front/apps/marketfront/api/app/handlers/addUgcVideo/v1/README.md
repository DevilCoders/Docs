# Резолвер addUgcVideo

## Описание

Резолвер передает в pers-author информацию о загруженном на видеохостинг видео, тем самым завершая его загрузку.

В ответе приходит статус загрузки: успех или ошибка.

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `videoId` | string | Айди видео, которое нам вернул видеохостинг | - |
| `title` | string |  Заголовок для видео | - |
| `productId` | ProductId| Сущность товара, к котрому привязано видео | - |
| `skuId` | SkuId |идентификатор товарной позиции  | - |

## Пример запроса

```text
curl --location --request POST 'https://<FAPI_URL>/api/v1/?name=addUgcVideo' \
--header 'Authorization: OAuth <Token>' \
--header 'Content-Type: application/json' \
--data-raw '{
    "params": [
        {
            "productId": 64428000,
            "skuId": 100256653696,
            "title": "A video title",
            "videoId": "7cabadc8-7f02-4e45-b06d-0d86c0d90415"
        }
    ]
}'
```

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addUgcVideo/v1/index.js)
- [Описание сущности `ugc-видео` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/ugcVideo/index.js)
