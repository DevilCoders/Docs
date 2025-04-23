# Резолвер resolveWishlistReflist

Резолвер для полчения упрощенного избранного

## Пример запроса

```
curl --location --request POST 'https://<FAPI_HOST>/api/v1?name=resolveWishlistReflist' \
--data-raw '{
	"params": [{}]
}'
```

Пример ответа

```json
{
    "results": [
        {
            "handler": "resolveWishlistReflist",
            "result": [
                "sku100252712412",
                "sku100252712412"
            ]
        }
    ],
    "collections": {
        "referenceWishlistItem": [
            {
                "id": "sku100252712412",
                "wishlistItemId": 101683082,
                "referenceId": "100252712412",
                "referenceEntity": "sku"
            }
        ]
    }
}
```

## Полезные ссылки:

- [Тип ответа](https://github.yandex-team.ru/market/beton/blob/1dff0fe4ccb3682ceb5d2105dcd890ab9deb321d/src/resolvers/wishlist/resolveWishlistReflist.js#L13)
