# Резолвер resolveWishlistTags

## Описание

Возвращет тэги пользователя для экземпляров «избранного»

## Параметры

Входных параметров нет. Пользователь должен быть авторизован

## Пример запроса
```sh
curl --request POST \
  --url '<FAPI host>/api/v1?name=resolveWishlistTags' \
  --header 'content-type: application/json' \
  --header 'x-user-authorization: OAuth <User OAuth token>' \
  --data '{"params": [{}]}'
```
## Пример ответа
```json
{
  "results": [
    {
      "handler": "resolveWishlistTags",
      "result": [
        234289779
      ]
    }
  ],
  "collections": {
    "wishlistTag": Array()
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveWishlistTags/v1/index.js)
- [Описание сущности `тэг` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/wishlistTag/index.js)
