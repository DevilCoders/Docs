# Адреса в паспорте
## HTTP API
### POST /address/create
user_id = id пользователя
user_type = тип пользователя (default user_type=passport паспортный пользователь)
address_type = тип адреса (default тип "address")

Тело запроса:
```json
{
  "building": 16,
  "comment": "Это мой домашний адрес.",
  "country": "Россия",
  "district": "string",
  "entrance": 2,
  "floor": 5,
  "intercom": 235,
  "locality": "Москва",
  "location": {
    "latitude": 0,
    "longitude": 0
  },
  "regionId": 213,
  "room": 16,
  "street": "ул. Льва Толстого",
  "type": "HOME",
  "zip": 119021
}
```
Тело ответа:
```json
{
  "status": "ok",
  "id": "string"
}
```
### POST /address/update
id - id контакта

Тело запроса:
```json
{
  
  "address_type": "address",
  "building": 16,
  "comment": "Это мой домашний адрес.",
  "country": "Россия",
  "district": "string",
  "entrance": 2,
  "floor": 5,
  "intercom": 235,
  "locality": "Москва",
  "location": {
    "latitude": 0,
    "longitude": 0
  },
  "regionId": 213,
  "room": 16,
  "street": "ул. Льва Толстого",
  "type": "HOME",
  "zip": 119021
}
```
Тело ответа:
```json
{
  "status": "ok",
  "id": "string"
}
```

### GET /address/delete
id = id контакта

Тело ответа:
```json
{
  "status": "ok",
  "id": "string"
}
```

### GET /address/get
id = id контакта

Тело ответа
```json
{
  "status": "ok",
  "id": "xxxxxxx",
  "address_type": "address",
  "building": 16,
  "comment": "Это мой домашний адрес.",
  "country": "Россия",
  "district": "string",
  "entrance": 2,
  "floor": 5,
  "intercom": 235,
  "locality": "Москва",
  "location": {
    "latitude": 0,
    "longitude": 0
  },
  "regionId": 213,
  "room": 16,
  "street": "ул. Льва Толстого",
  "type": "HOME",
  "zip": 119021
}
```

### GET /address/list
user_id = id пользователя
user_type = тип пользователя (default user_type=passport паспортный пользователь)
length - число адресов в выдаче
offset - оффсет

```json
{
  "more": "true",
  "addresses": [
    {
      "addressId": "string",
      "building": 16,
      "comment": "Это мой домашний адрес.",
      "country": "Россия",
      "district": "string",
      "entrance": 2,
      "floor": 5,
      "id": "string",
      "intercom": 235,
      "lastTouchedTime": "2021-08-03T08:21:44.857Z",
      "locality": "Москва",
      "location": {
        "latitude": 0,
        "longitude": 0
      },
      "regionId": 213,
      "room": 16,
      "street": "ул. Льва Толстого",
      "type": "HOME",
      "zip": 119021
    }
  ]
}
```