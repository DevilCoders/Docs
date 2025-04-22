# Резолвер saveWishlistTags

## Описание

Изменяет тэги пользователя для экземпляров «избранного»

## Параметры

Пользователь должен быть авторизован. На вход передаём массив объектов с названием и id

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `tags`* | array | Массив объектов с названием тега и его id | - | - |

\* - обязательный параметр


## Пример запроса
```sh
curl --request POST \
  --url '<FAPI host>api/v1?name=saveWishlistTags' \
  --header 'content-type: application/json' \
  --header 'x-user-authorization: OAuth <User OAuth token>' \
  --data '{
    "params": [{
        "tags": [{
            "id": 234289740,
            "displayName": "test"
        }]
    }]
}'
```

## Пример ответа

```json
{
  "results": [
    {
      "handler": "saveWishlistTags",
      "result": []
    }
  ],
  "collections": {
    "wishlistTag": Array()
  }
}

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/saveWishlistTags/v1/index.js)
- [Описание сущности `тэг` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/wishlistTag/index.js)

```
