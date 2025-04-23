# Резолвер resolveWishlistItemsWithReferences

Резолвер для полчения нового сравнения с сущностями

\* - Обязательный параметр

## Параметры из тела запроса

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `pageSize` | number | количество элменетов на странице | - |
| `token` | object | токен идентификатора странцы, получается после первого запроса к ручке | - |
| `token.lastCrTime` | sting | последнее обновление | - |
| `token.lastId` | sting | последняя добавленная сущность | - |

## Пример запроса

```
curl --location --request POST 'https://<FAPI_HOST>/api/v1?name=resolveWishlistItemsWithReferences' \
--data-raw '{
	"params": [{}]
}'
```

## Полезные ссылки:

- [Тип ответа](https://github.yandex-team.ru/market/market/blob/ba914001b069f9603365c94c98cfce4189c2370c/src/resolvers/wishlist/resolveWishlistItemsWithReferences.js#L29)
- [Тип параметров](https://github.yandex-team.ru/market/beton/blob/3a101a7255442d4cd8ea10d42745029a39ab611c/src/resources/wishlist/params/index.js#L57)
