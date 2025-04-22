## Резолвер resolveProfitIndexEntry

Ручка получения данных для точки входа индекса выгодности


## Пример запроса


```text
curl --location --request POST 'https://front-market-unified--marketfront-54590-prestableapi.demofslb.beru.ru/api/v1?name=resolveProfitIndexEntry' \
--header 'api-platform: ANDROID' \
--data-raw '{
	"params": {}
}'
```

## Пример ответа

```json
{
    "results": [
        {
            "handler": "resolveProfitIndexEntry",
            "result": {
                "indexValue": 9.20321083,
                "yesterdayIndexDiff": 0.327662468,
                "indexStructure": {
                    "priceValue": 1.5,
                    "discountValue": 1.5,
                    "promoValue": 1.5,
                    "cashbackValue": 1.5
                },
                "categories": [
                    {
                        "image": "//avatars.mds.yandex.net/get-mpic/4322107/img_id8962600163296697049.jpeg/orig",
                        "imageHd": "//avatars.mds.yandex.net/get-mpic/4322107/img_id8962600163296697049.jpeg/orig"
                    },
                    {
                        "image": "//avatars.mds.yandex.net/get-mpic/4489193/img_id7820413109299165800.jpeg/orig",
                        "imageHd": "//avatars.mds.yandex.net/get-mpic/4489193/img_id7820413109299165800.jpeg/orig"
                    },
                    {
                        "image": "//avatars.mds.yandex.net/get-mpic/3765589/img_id6658168663792038917.jpeg/orig",
                        "imageHd": "//avatars.mds.yandex.net/get-mpic/3765589/img_id6658168663792038917.jpeg/orig"
                    },
                    {
                        "image": "//avatars.mds.yandex.net/get-mpic/4561793/img_id6270739844950654824.jpeg/orig",
                        "imageHd": "//avatars.mds.yandex.net/get-mpic/4561793/img_id6270739844950654824.jpeg/orig"
                    }
                ]
            }
        }
    ],
    "collections": {}
}
```

## Полезные ссылки
[Документация на ручки mars'а](https://wiki.yandex-team.ru/mars/)
