# Резолвер deleteWishlistItem

Резолвер для полчения общего сравнения

\* - Обязательный параметр

## Параметры из query запроса

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `uuid`* | string | идентификатор установки приложения | - |

## Параметры из тела запроса

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `id`* | number | id элемента | - |

## Пример запроса

```
curl --location --request POST 'https://<FAPI_HOST>/api/v1?name=deleteWishlistItem' \
--data-raw '{
	"params": [{
		"id": 101681348
	}]
}'
```

## Пример ответа

```json
{
    "results": [
        {
            "handler": "deleteWishlistItem",
            "result": {
              "total": 1, // оставшееся количество элементов
              "wishlistItemId": "123" // id удаленного элемента
            }
        }
    ],
    "collections": {}
}
```
