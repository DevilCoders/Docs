# Дополнительные поля для доставки/еды

## 1. Ручки из userplaces
В ответах ручек /userplace/item, /userplaces/list, /3.0/userplaces имеем
дополнительные поля floor_number (этаж), quarters_number (квартира/офис)

/3.0/userplaces response
​```
{
    "places": [
        {
            "id": "560d20857e924d6b8615f6b17d872b34",
            "version": 1,
            "name": "HOME",
            "porchnumber": "2",
            "floor_number": "10",
            "quarters_number": "119",
            "comment": "Комментарий",
            "place_type": "home",
            "uri": "uri://example",
            "address": {
                "oid": "8060029",
                "uri": "uri://example",
                "city": "Moscow",
                "description": "Moscow, Russian Federation",
                "full_text": "Russian Federation, Moscow, Petrovsky Boulevard, 21",
                "point": [
                    37.619046,
                    55.767843
                ],
                "house": "21",
                "object_type": "другое",
                "exact": true,
                "street": "Petrovsky Boulevard",
                "country": "Russian Federation",
                "short_text": "Petrovsky Boulevard, 21",
                "type": "address",
                "comment": "Комментарий",
                "floor_number": "10",
                "quarters_number": "119",
                "porchnumber": "3"
            }
        }
    ]
}
​```

/userplaces/list response
​```
{
  "places": [
    {
      "id": "560d20857e924d6b8615f6b17d872b34",
      "version": 123,
      "created": "2018-02-01T11:22:33+0000",
      "updated": "2019-02-01T11:22:33+0000",
      "name": "Дом",
      "place_type": "home",
      "porchnumber": "45",
      "floor_number": "10",
      "quarters_number": "119",
      "full_text": "Россия, Москва, Петровский бульвар, 21",
      "short_text": "Петровский бульвар, 21",
      "description": "Россия, Москва",
      "point": [
        37.619046,
        55.767843
      ],
      "uri": "yamaps://12345",
      "type": "address"
    },
    {
      "id": "360d20857e024d6b8615f6b17d872b34",
      "version": 123,
      "created": "2018-02-01T11:22:33+0000",
      "updated": "2019-02-01T11:22:33+0000",
      "name": "Работа",
      "place_type": "work",
      "porchnumber": "45",
      "full_text": "Россия, Москва, Петровский бульвар, 22",
      "short_text": "Петровский бульвар, 22",
      "description": "Россия, Москва",
      "point": [
        37.619046,
        55.767843
      ]
    }
  ]
}
​```

/userplaces/item response
​```
{
  "id": "560d20857e924d6b8615f6b17d872b34",
  "version": 123,
  "created": "2018-02-01T11:22:33+0000",
  "updated": "2019-02-01T11:22:33+0000",
  "name": "Дом",
  "place_type": "home",
  "porchnumber": "45",
  "floor_number": "10",
  "quarters_number": "119",
  "full_text": "Россия, Москва, Петровский бульвар, 21",
  "short_text": "Петровский бульвар, 21",
  "description": "Россия, Москва",
  "point": [
    37.619046,
    55.767843
  ],
  "uri": "yamaps://12345",
  "type": "address"
}
​```

request to /3.0/userplacesupdate
​```
{
    "id": "300ab85fbcc54eb49438e0e39bab040c",
    "places": [
        {
            "id": "16fd261107aa43eb96582b049d68b1c4",
            "version": 1,
            "name": "HOME",
            "address": {
                "description": "Москва, Россия",
                "full_text": "Россия, Москва, Петровский бульвар, 21",
                "point": [
                    37.619046,
                    55.767843
                ],
                "house": "21",
                "object_type": "другое",
                "street": "Петровский бульвар",
                "short_text": "Петровский бульвар, 21",
                "exact": true,
                "city": "Москва",
                "country": "Россия",
                "type": "address",
                "floor_number": "10",
                "quarters_number": "119",
                "uri": "some uri"
            }
        }
    ]
}
​```

## 2. Ручки из persuggest
В элементах массива results ручек /4.0/persuggest/v1/finalsuggest и 
/4.0/persuggest/v1/zerosuggest эти же поля

result in /4.0/persuggest/v1/zerosuggest response
​```
"results": [
    {
        "lang": "ru",
        "log": "",
        "action": "userplace",
        "position": [37, 55],
        "floor_number": "10",
        "quarters_number": "119",
        "subtitle": {
            "hl": [],
            "text": "Петровский бульвар, 21"
        },
        "text": "Москва, Россия",
        "title": {
            "hl": [],
            "text": "u1"
        },
        "uri": "test_uri_u1",
        "userplace_info": {
            "id": "00000004-AAAA-AAAA-AAAA-000000000001",
            "name": "U1",
            "version": 123
        }
    },
    {
        "lang": "ru",
        "log": "",
        "action": "ml_prediction",
        "position": [37.588458, 55.733959],
        "subtitle": {
            "hl": [],
            "text": "Okhotny Ryad Street"
        },
        "text": "Russia, Moscow, Lva Tolstogo Street, 16",
        "title": {
            "hl": [],
            "text": "Russian Federation, Moscow, Okhotny Ryad Street"
        },
        "uri": "some uri"
    }
]
​```

results in /4.0/persuggest/v1/finalsuggest response
​```
"results": [
    {
        "comment": "Нужна сдача с 5000р",
        "point_id": "3b6c041a-ac8a-11e8-ab7a-c519f77d42bf",
        "lang": "rus",
        "log": "{some log}",
        "method": "userplace",
        "entrance": "2",
        "floor_number": "10",
        "quarters_number": "119",
        "position": [37.595081, 54.196766],
        "subtitle": {
            "hl": [],
            "text": "Тула, Россия"
        },
        "text": "Россия, Тула, улица Клары Цеткин, 4 ",
        "title": {
            "hl": [[0, 5], [6, 11], [12, 18]],
            "text": "улица Клары Цеткин, 4"
        },
        "uri": "some uri"
    },
],
​```

