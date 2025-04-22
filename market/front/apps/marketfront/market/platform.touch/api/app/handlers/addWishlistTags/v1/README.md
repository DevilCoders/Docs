# Резолвер addWishlistTags

## Описание

Добавляет тэги пользователя для экземпляров «избранного»

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `tags`* | array | Массив объектов с названием тега | - | - |

\* - обязательный параметр

## Пример запроса
```sh
curl --request POST \
  --url '<FAPI host>/api/v1?name=addWishlistTags' \
  --header 'content-type: application/json' \
  --header 'x-user-authorization: OAuth <User OAuth token>' \
  --data '{
    "params": [{
        "tags": [{
            "displayName": "foo"
        }]
    }]
}'
```

## Пример ответа

```json
{
  "results": [
    {
      "handler": "addWishlistTags",
      "result": [
        234289786
      ]
    }
  ],
  "collections": {
    "wishlistTag": Array()
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addWishlistTags/v1/index.js)
- [Описание сущности `тэг` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/wishlistTag/index.js)
