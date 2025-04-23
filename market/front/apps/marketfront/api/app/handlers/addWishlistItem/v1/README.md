# Резолвер addWishlistItem

Резолвер для для добавления в сравнение

\* - Обязательный параметр

## Параметры из query запроса

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `uuid`\* | string | идентификатор установки приложения | - |

## Параметры из тела запроса

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `referenceEntity`\* | string | тип элемента | - |
| `referenceId`\* | string | id элемента | - |
| `title`\* | string | id элемента | - |

## Пример запроса

```
curl --location --request POST 'https://<FAPI_URL>/api/v1?name=addWishlistItem' \
--data-raw '{
	"params": [{
                "id": 101681412,
                "referenceEntity": "sku",
                "referenceId": "100252712412",
                "referenceWishlistItemId": "sku100252712412",
                "secondaryReferences": {},
                "title": "Компьютерное кресло Chairman PRESTIGE ERGO, обивка: текстиль, цвет:",
                "addedAt": "2020-10-22T19:28:02.816559Z",
                "price": {
                    "value": 9999,
                    "currency": "RUR"
                },
                "picture": "//avatars.mds.yandex.net/get-mpic/364668/img_id6630159530891598311/orig",
                "rgb": "white"
            }]
}'
```

## Пример ответа

```json
{
    "results": [
        {
            "handler": "addWishlistItem",
            "result": [
                101681590
            ]
        }
    ],
    "collections": {
        "wishlistItem": [
            {
                "id": 101681590,
                "referenceEntity": "sku",
                "referenceId": "100252712412",
                "referenceWishlistItemId": "sku100252712412",
                "secondaryReferences": {},
                "title": "Компьютерное кресло Chairman PRESTIGE ERGO, обивка: текстиль, цвет:",
                "addedAt": "2020-10-22T19:28:02.816559Z",
                "price": {
                    "value": 9999,
                    "currency": "RUR"
                },
                "picture": "//avatars.mds.yandex.net/get-mpic/364668/img_id6630159530891598311/orig"
            }
        ]
    }
}
```
