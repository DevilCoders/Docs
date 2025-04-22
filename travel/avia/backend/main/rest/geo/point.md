# Описание ручки
Ручка возвращает settlement и station по point_key.

## Формат запроса:
```
curl -X GET <API-HOST>/rest/geo/point?<key>&<geo_id>&<lang>
```
*key* - point_key в формате  c... ,  s...

key и geo_id не могут быть в запросе одновременно
## Формат ответа:

```
/rest/geo/point?key=s9600370&lang=ru
{
    "status": "ok",
    "data":
        {
            "station":
            {
                "urlTitle":"Kol'tsovo123",
                "iataCode":"SVX",
                "popularTitle":"Кольцово123",
                "sirenaCode":"КЛЦ",
                "phraseFrom":"Кольцово",
                "title":"Кольцово123",
                "regionId":11162,
                "phraseIn":"Кольцово",
                "phraseTo":"Кольцово",
                "id":9600370,
                "t_type":2,
                "longitude": 60.804833,
                "latitude": 56.750107
            },
            "settlement":
            {
                "countryId":225,
                "phraseFrom":"Екатеринбурга",
                "urlTitle":"Ekaterinburg",
                "title":"Екатеринбург",
                "phraseIn":"Екатеринбурге",
                "iata":"SVX",
                "phraseTo":"Екатеринбург",
                "id":54,
                "geoId":54,
                "longitude": 60.804833,
                "latitude": 56.750107
            }
        }
    }
}
```


```
/rest/geo/point?key=c213&lang=ru
{
   "status": "ok",
   "data":
   {
        "station":null,
        "settlement":
            {
                "countryId":225,
                "phraseFrom":"Москвы",
                "urlTitle":"Moskva"",
                "title":"Москва"",
                "phraseIn":"Москве",
                "iata":"MOW",
                "phraseTo":"Москву",
                "id":213,
                "geoId":213,
                "longitude": 60.804833,
                "latitude": 56.750107
            }
   }
}
```
