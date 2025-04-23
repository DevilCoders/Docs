# Резолвер resolvePrescription

## Описание

хендлер вызывающий резолвер resolvePrescription, который вызывает ресурс fetchPrescription. обращается к бекэнду http://check-erx-service.tst.vs.market.yandex.net

https://wiki.yandex-team.ru/check-erx-service/check-erx-service-internal/post/checkDrugs2/


## Пример запроса

```bash
curl -X POST 'https://[FAPI_HOST]/api/v1?name=resolvePrescription' \
-H 'Content-Type: application/json' \
-H 'X-User-Authorization: OAuth AQAAAADu-WeeAAAKiYi-bmjyjUb0ikd4i28BWUk' \
-H 'api-platform: ANDROID' \
-H 'cache-control: no-cache' \
-d '{
    "params": [
        {
            "isFakeMedicata": true,
            "isFakeReport": true,
            "query":{
                "items": [                             
                    {              
                        "offerId": "wNf7Z9Gsmf3_aFQwBQf_og",
                        "quantity": 12.0,
                        "name": "Интерферон альфа-2b р-р д/ин. 1000000МЕ",
                        "tradeName": "Интерферон альфа-2b р-р д/ин. 1000000МЕ"
                    },
                    {
                        "offerId": "wNf7Z9Gsmf3_aFQwAQf_og",
                        "quantity": 2.0,
                        "name": "Золототысячника трава сырье растит. пор.",
                        "tradeName": "Золототысячника трава сырье растит. пор."
                    }
                ],
                "uid": 1,
                "regionId": 123,
                "userEsiaToken": "b3ec53e1-c7d1-4829-ba2d-ce01f00e4a26"
            }
        }
    ]
}'
```