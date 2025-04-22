# Описание ручки
Ручка возвращает список популярных направлений с мин.ценами по geo_id.

## Формат запроса:
```
GET /rest/travel-recipes?from_geo_id=54&national_version=ru&forward_date=2019-07-15&limit=2
```

Необязательные параметры:

forward_date : по умолчанию environment.now()
backward_date : по умолчанию отсутствует
limit : по умолчанию 5

Выбор окна поиска цен:

- если задана forward_date, то 1 день
- если не задано, то 30 дней 


## Формат ответа:
```
GET http://<host>/rest/travel-recipes?from_geo_id=54&national_version=ru&forward_date=2019-07-15&limit=1
{
    "status": "ok",
    "data": [
        {
            "forward_date": "2019-07-16",
            "to_id": 2,
            "settlement_to": {
                "countryId": 225,
                "phraseFrom": "Санкт-Петербурга",
                "urlTitle": "Sankt-Peterburg",
                "title": "Санкт-Петербург",
                "phraseIn": "Санкт-Петербурге",
                "iata": "LED",
                "phraseTo": "Санкт-Петербург",
                "id": 2,
                "geoId": 2
            },
            "min_price": {
                "currency": "RUR",
                "value": 6170
            },
            "settlement_from": {
                "countryId": 225,
                "phraseFrom": "Екатеринбурга",
                "urlTitle": "Ekaterinburg",
                "title": "Екатеринбург",
                "phraseIn": "Екатеринбурге",
                "iata": "SVX",
                "phraseTo": "Екатеринбург",
                "id": 54,
                "geoId": 54
            },
            "image": "https://avatars.mdst.yandex.net/get-avia/4277/2a0000015c87cf5bed25291f1ef28a60e151",
            "from_id": 54
        }
    ]
}
```
