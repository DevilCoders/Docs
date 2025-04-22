# Описание ручки
Ручки возвращают информацию о странах.

## Формат запроса:
```
curl -X GET <API-HOST>/geo/country/<country_id>
Если не указать country_id - вернет все страны
curl -X GET <API-HOST>/geo/country
```
*country_id* - id страны

Optional:
- lang=[string], default lang=ru
- fields=[string] - указание полей для получения. Поля передаются список через запятую, например "?fields=id,title". Если поле не передано, возвращаются все поля. Можно запрашивать поля: `id,code,point_key,title`
## Формат ответа:

/rest/geo/country/21477
```
{
   "status": "ok",
   "data": {
       "title": "Гайана",
       "code": "GY",
       "id": 21477,
       "point_key": "l21477",
       "geo_id": 21477
   }
}
```

Запрос фильтров полей и языком: /rest/geo/country/21477?lang=tr&fields=id,title
```
{
    "status": "ok",
    "data": {
        "id": 21477,
        "title": "Guyana"
    }
}
```

Запрос фильтров полей и языком для всех АК: /rest/airlines/airline_info?lang=ru&fields=title,point_key,code
```
{
    "status": "ok",
    "data": {

        ...

        "21331": {
            "title": "Чад",
            "code": "TD",
            "point_key": "l21331"
        },
        "20989": {
            "title": "Эритрея",
            "code": "ER",
            "point_key": "l20989"
        }
    }
}
```
