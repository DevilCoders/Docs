# Резолвер removeWishlistTags

## Описание

Удаляет тэги пользователя для экземпляров «избранного»

## Входные парметры

Пользователь должен быть авторизован. На вход передаём массив id тэгов

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `tagIds`* | array | Массив id тэгов | - | - |

\* - обязательный параметр

## Пример запроса
```sh
curl --request POST \
  --url '<FAPI host>/api/v1?name=removeWishlistTags' \
  --header 'content-type: application/json' \
  --header 'x-user-authorization: OAuth <User OAuth token>' \
  --data '{
    "params": [{
        "tagIds": [234289713,
            234289671,
            234289673,
            234289729,
            234289675,
            234289730,
            234289678]
	}]
}'
```

## Пример ответа

```json
{
  "results": [
    {
      "handler": "removeWishlistTags",
      "result": []
    }
  ],
  "collections": {
    "wishlistTag": Array()
  }
}

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/removeWishlistTags/v1/index.js)
- [Описание сущности `тэг` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/wishlistTag/index.js)
