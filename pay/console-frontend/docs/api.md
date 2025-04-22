# API

**Предусмотреть**
1. Все ручки кроме GET должны будут подписываться CSRF-токеном. Он будет приходить в `window.__CONFIG.csrfToken`.
2. Имена речек и схема ответов может меняться. Нужно предусмотреть слой абстракции отделяющий данные АПИ от данных приложения.
3. Заложить возможность декорировать ручки.




## Стандартный ответ с ошибкой
**Response**
```json
{
  "status": "fail",
  "code": "<http-status-code>",
  "data": {
    "message": "string",
  }
}
```

## GET /api/web/v1/partners/suggest?q=yandex

**Response**
```json
{
  "status": "success",
  "code": 200,
  "data": [
    {
        "inn": "7736207543",
        "ogrn": "1027700229193",
        "name": "ЯНДЕКС, ООО",
        "address": "119021, г. Москва, ул. Льва Толстого, д. 16",
        "full_name": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ  ЯНДЕКС",
        "region_name": "Москва",
        "leader_name": "Бунина Елена Игоревна",
    },
    {
        "inn": "7704357909",
        "ogrn": "1167746491395",
        "name": "ЯНДЕКС.МАРКЕТ, ООО",
        "address": "121099, г. Москва, бульвар Новинский, д. 8 пом. 9.03 этаж 9",
        "full_name": "ОБЩЕСТВО С ОГРАНИЧЕННОЙ ОТВЕТСТВЕННОСТЬЮ  ЯНДЕКС.МАРКЕТ",
        "region_name": "Москва",
        "leader_name": "Гришаков Максим Петрович",
    },
  ]
}
```

## POST /api/web/v1/partners

**Request**
```json
{
  "name": "string",
  "registration_data": {
    "contact": {
      "phone": "string",
      "email": "string",
      "name": "string",
    },
    "inn": "string",
    "ogrn": "string",
    "address": "string",
    "full_name": "string",
    "region_name": "string",
    "leader_name": "string",
  }
}
```

**Response**
```json
{
  "status": "success",
  "code": 200,
  "data": {
    "partner_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "merchant_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "updated": "2022-04-07T07:54:06.806Z",
    "created": "2022-04-07T07:54:06.806Z",
    "name": "string"
  }
}
```

## POST /api/web/v1/partners/{partner_id}/merchants

**Request**
```json
{
  "name": "string"
}
```

**Response**
```json
{
  "status": "success",
  "code": 200,
  "data": {
    "partner_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "created": "2022-03-17T08:19:19.536Z",
    "name": "string",
    "merchant_id": "25c1d927-6a8a-4e58-a73d-4a72c0e4ff20",
    "updated": "2022-03-17T08:19:19.536Z"
  }
}
```

## POST /api/web/v1/partners/{partner_id}/merchants/{merchant_id}/origins

**Request**
```json
{
  "origin": "string"
}
```

**Response**
```json
{
  "status": "success",
  "code": 200,
  "data": {
    "layouts": [
      {
        "document": {
          "mime": "string",
          "created": "2022-04-07T07:54:06.812Z",
          "updated": "2022-04-07T07:54:06.812Z",
          "document_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "name": "string"
        },
        "layout_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "origin_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "created": "2022-04-07T07:54:06.812Z",
        "updated": "2022-04-07T07:54:06.812Z",
        "type": "string"
      }
    ],
    "partner_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "moderation": {
      "approved": true,
      "resolved": true,
      "origin_id": "string",
      "created": "2022-04-07T07:54:06.812Z",
      "origin_moderation_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "updated": "2022-04-07T07:54:06.812Z"
    },
    "merchant_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "created": "2022-04-07T07:54:06.812Z",
    "origin": "string",
    "origin_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "updated": "2022-04-07T07:54:06.812Z"
  }
}
```

## POST /api/web/v1/merchants/{merchant_id}/integrations

**Request**
```json
{
  "psp_external_id": "string",
  "status": "string",
  "creds": "string",
  "encrypted": false,
  "for_testing": true
}
```

Для Payture:
```json
{
  "psp_external_id": "payture",
  "creds": "{\"key\": \"YandexPayTest3DS\", \"password\": \"123\", \"gateway_merchant_id\": \"YandexPayTest3DS\"}",
  "encrypted": false,
}
```

**Response**
```json
{
  "status": "success",
  "code": 200,
  "data": {
    "integration_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "for_testing": true,
    "revision": 0,
    "psp_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "created": "2022-04-07T07:53:28.482Z",
    "updated": "2022-04-07T07:53:28.482Z",
    "merchant_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "status": "string"
  },
}
```

## GET /api/web/v1/geo/suggest?q=льва

**Response**
```json
{
  "status": "success",
  "code": 200,
  "data": [
    {
      "type": "toponym",
      "log_id": {
        "server_reqid": "1648648061147198-3182013194-suggest-maps-hamster-yp-9",
        "pos": 0,
        "type": "toponym",
        "where": {
          "name": "Россия, Москва, улица Льва Толстого",
          "source_id": "8059948",
          "title": "улица Льва Толстого"
        }
      },
      "personalization_info": {
        "server_reqid": "1648648061147198-3182013194-suggest-maps-hamster-yp-9",
        "pos": 0,
        "type": "toponym",
        "where": {
          "name": "Россия, Москва, улица Льва Толстого",
          "source_id": "8059948",
          "title": "улица Льва Толстого"
        }
      },
      "title": {
        "text": "улица Льва Толстого",
        "hl": [
          [6, 10]
        ]
      },
      "subtitle": {
        "text": "Москва, Россия",
        "hl": []
      },
      "text": "Россия, Москва, улица Льва Толстого ",
      "tags": ["street"],
      "action": "substitute",
      "uri": "ymapsbm1:\/\/geo?ll=37.586674%2C55.733986&spn=0.008705%2C0.005310&text=%D0%A0%D0%BE%D1%81%D1%81%D0%B8%D1%8F%2C%20%D0%9C%D0%BE%D1%81%D0%BA%D0%B2%D0%B0%2C%20%D1%83%D0%BB%D0%B8%D1%86%D0%B0%20%D0%9B%D1%8C%D0%B2%D0%B0%20%D0%A2%D0%BE%D0%BB%D1%81%D1%82%D0%BE%D0%B3%D0%BE%20",
      "distance": {
        "value": 7054258.821,
        "text": "7054.26 км"
      }
    },
    {
      "type": "toponym",
      "log_id": {
        "server_reqid": "1648648061147198-3182013194-suggest-maps-hamster-yp-9",
        "pos": 1,
        "type": "toponym",
        "where": {
          "name": "Россия, Москва, улица Льва Толстого, 16",
          "source_id": "56697621",
          "title": "улица Льва Толстого, 16"
        }
      },
      "personalization_info": {
        "server_reqid": "1648648061147198-3182013194-suggest-maps-hamster-yp-9",
        "pos": 1,
        "type": "toponym",
        "where": {
          "name": "Россия, Москва, улица Льва Толстого, 16",
          "source_id": "56697621",
          "title": "улица Льва Толстого, 16"
        }
      },
      "title": {
        "text": "улица Льва Толстого, 16",
        "hl": [
          [6, 10]
        ]
      },
      "subtitle": {
        "text": "Москва, Россия",
        "hl": []
      },
      "text": "Россия, Москва, улица Льва Толстого, 16 ",
      "tags": ["house"],
      "action": "search",
      "uri": "ymapsbm1:\/\/geo?ll=37.587093%2C55.733974&spn=0.001000%2C0.001000&text=%D0%A0%D0%BE%D1%81%D1%81%D0%B8%D1%8F%2C%20%D0%9C%D0%BE%D1%81%D0%BA%D0%B2%D0%B0%2C%20%D1%83%D0%BB%D0%B8%D1%86%D0%B0%20%D0%9B%D1%8C%D0%B2%D0%B0%20%D0%A2%D0%BE%D0%BB%D1%81%D1%82%D0%BE%D0%B3%D0%BE%2C%2016%20",
      "distance": {
        "value": 7054276.057,
        "text": "7054.28 км"
      }
    }
  ]
}
```
