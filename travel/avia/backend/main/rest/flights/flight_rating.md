# Описание ручки
Ручка возвращает статистику по рейсу.



## Формат запроса:
```
curl -X GET <API-HOST>/rest/flights/flight_rating/<flight_number>
```
*flight_number* - номер рейса (через дефис)

## Формат ответа:

```
/rest/flights/flight_rating/SU-12
{
    "status":"ok",
    "data":
    {
        "delayedLess30":0,
        "delayed3060":0,
        "avgScore":10.0,
        "badPercent":0,
        "delayedMore90":0,
        "canceled":0,
        "goodCount":29,
        "scores":290,
        "delayed6090":0,
        "outrunning":41,
        "badCount":0
    }
}
```

Если рейса не нашлась, возвращаем null.
```
{
   "status": "ok",
   "data": null
}
```