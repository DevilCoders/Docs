# Описание ручки
Ручка возвращает все праздники, для каждого праздника есть название, id и список оцененных перевозок на даты (3 минимальные цены на направление и +/- 2дня)

## Формат запроса:
```
'/rest/holidays/<national_version>/<lang>/<holiday_id>/from_city/<from_city_id>'
```
*holiday_id* - идентификатор праздника
*from_city_id* - идентификатор города отправления
*national_version* - национальная версия
*lang* - язык

## Формат ответа:

```
https://<host>/rest/holidays/ru/en/1/from_city/2
{
    "status": "ok",
    "data": {
        "directionVariants": [
            {
                "price": {
                    "currency": "RUR",
                    "value": 11840
                },
                "backwardDate": "2018-01-05",
                "fromCity": {
                    "code": "SVX",
                    "phraseFrom": "Yekaterinburg",
                    "key": "c54",
                    "urlTitle": "Yekaterinburg",
                    "country": {
                        "urlTitle": "Russia",
                        "id": 225,
                        "title": "Russia"
                    },
                    "title": "Yekaterinburg",
                    "iataCode": "SVX",
                    "id": 54
                },
                "forwardDate": "2017-12-29",
                "toCity": {
                    "code": "LED",
                    "phraseFrom": "Saint-Petersburg",
                    "key": "c2",
                    "urlTitle": "Saint-Petersburg",
                    "country": {
                        "urlTitle": "Russia",
                        "id": 225,
                        "title": "Russia"
                    },
                    "title": "Saint-Petersburg",
                    "iataCode": "LED",
                    "id": 2
                },
                "image": {
                    "id": 23,
                    "url2": "https://avatars.mds.yandex.net/get-avia/163457/2a0000015ca1fcd31c9fa4ef45a8dbf349f7"
                }
            }
        ],
        "endDay": "2018-01-07",
        "startDay": "2017-12-31",
        "nameTankerKey": "holiday_3",
        "id": 3
    }
}
```
