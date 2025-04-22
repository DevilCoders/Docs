Формат запроса-ответа согласно https://wiki.yandex-team.ru/passport/takeout/integration/#zapros
`curl -X POST "http://{{ API_HOST}}/takeout/v1.0/mobile_api_user" -d "uid=1&unixtime=123456789" -H "X-Ya-Service-Ticket: smth"`
#### Успешные запросы
CODE: 200
```json
{"status":"no_data"}
```
CODE: 200
```json
{
  "status": "ok",
  "data": {
    "favorites.json": "[{\"passengers\":{\"infants\":0,\"adults\":1,\"children\":0},\"point_from_key\":\"c54\",\"point_to_title\":\"\\u0415\\u0440\\u0435\\u0432\\u0430\\u043d\",\"forward_date\":\"2019-05-09\",\"point_to_key\":\"c10262\",\"point_from_title\":\"\\u0415\\u043a\\u0430\\u0442\\u0435\\u0440\\u0438\\u043d\\u0431\\u0443\\u0440\\u0433\",\"backward_date\":null}]",
    "flights.json": "[{\"departure_date\":\"2018-11-08\",\"number\":\"SU 6402\"},{\"departure_date\":\"2019-10-16\",\"number\":\"SU 100\"}]"
  }
}
```

#### При обращении с неверным, устаревшим или вообще без service ticket возможны ответы:
CODE: 403
```json
{"status":"fail","data":{"description":"Empty tvm service ticket"}}
```
CODE: 403
```json
{"status":"fail","data":{"description":"Access for service=1 is not allowed"}}
```
CODE: 401
```json
{"status":"fail","data":{"description":"TvmError: Some error"}}
```

#### При внутренних ошибках приложения
CODE 500
```json
{"status":"error","message":"Error id: 190219-112315-877-9bb8a"}
```
