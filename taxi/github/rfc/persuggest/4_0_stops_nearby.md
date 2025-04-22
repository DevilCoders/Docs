Получение точек посадки или высадки возле остановок
общественного транспорта на заданном удалении от точки.
Получение станций метро для абонемента (MAAS).


## Ручка /4.0/persuggest/v1/stops_nearby

Подразумевается использование при планировании поездки
от или до остановки на заданном удалении от пользователя.
В перспективе для поездки от остановки может добавиться учёт
возможности ожидания пассажира на месте посадки.
Пользователю предлагаются удобные точки посадки
для остановок, выбранных по критериям запроса.


Алгоритм сортировки станций можно задать конфигом 3.0.
Варианты:
- N1 станций из истории поездок пользователя, затем
  N2 ближайших станций с каждой ветки в радиусе поиска,
  затем остальные, отсортированные
  по расстоянию, расположению или по алфавиту
  с группировкой по ветке или без неё (4 параметра)


Линии и пикап поинты передаются отдельным дедуплицированным списком
и адресуются из остальных объектов по уникальному айдишнику.
Причина такого решения:
- линий метро всего около 20, и если добавлять полное описание в каждую
станцию, ответ сильно увеличится в объёме.
- пикап поинт может быть довольно большой структурой, и многие из них
будут использованы несколько раз.
Ниже некоторые примеры выходов, для которых пикап поинты будут повторяться:
  - часто выходы из метро расположены очень близко (лестницы в
  противоположных направлениях)
  - станции с пересадками имеют сквозную нумерацию выходов, что означает
  идентичные пикап поинты в разных объектах станций


```yaml
paths:
    /internal/persuggest/v1/stops_nearby:
        post:
            summary: |
                Получение ближайших остановок общественного транспорта
                и точек посадки рядом с ними.
            description: |
                ### Описание

                Подразумевается использование при планировании поездки
                от или до остановки на заданном удалении от пользователя.
                В перспективе для поездки от остановки может добавиться учёт
                возможности ожидания пассажира на месте посадки.
                Пользователю предлагаются удобные точки посадки
                для остановок, выбранных по критериям запроса.

                ### Пример

                #### Request

                {
                  "position": [37.538640, 55.750370],
                  "distance_meters": 1500,
                  "point_type": "b",
                  "transport_types": [
                    "metro"
                  ],
                  "locale": "ru_RU"
                }

                #### Response
                {
                  "stops": [
                    {
                      "transport_types": [
                        "metro"
                      ],
                      "common": {
                        "id": "1727707971",
                        "name": "Деловой центр",
                        "line_ids": [
                          "1727497101"
                        ]
                      },
                      "exits": [
                        {
                          "name": "Деловой центр",
                          "id": "1727708091",
                          "position": [
                            37.532903587,
                            55.747904065
                          ],
                          "pickup_point_id": "32570194"
                        },
                        {
                          "name": "Деловой центр",
                          "id": "4079120975",
                          "position": [
                            37.532972089,
                            55.747637737
                          ],
                          "pickup_point_id": "32570194"
                        }
                      ]
                    },
                    {
                      "transport_types": [
                        "metro"
                      ],
                      "common": {
                        "id": "station__9858852",
                        "name": "Международная",
                        "line_ids": [
                          "100000127"
                        ]
                      },
                      "exits": [
                        {
                          "name": "Международная",
                          "id": "1635140850",
                          "position": [
                            37.533330477,
                            55.748707636
                          ],
                          "pickup_point_id": "48382785"
                        },
                        {
                          "name": "Международная",
                          "id": "3370929415",
                          "position": [
                            37.533436166,
                            55.748348528
                          ],
                          "pickup_point_id": "32570194"
                        },
                        {
                          "name": "Международная",
                          "id": "100128259",
                          "position": [
                            37.533567035,
                            55.747885774
                          ],
                          "pickup_point_id": "41553621"
                        },
                        {
                          "name": "Международная",
                          "id": "2171714232",
                          "position": [
                            37.535768957,
                            55.747769672
                          ],
                          "pickup_point_id": "42443627"
                        }
                      ]
                    },
                    {
                      "transport_types": [
                        "metro"
                      ],
                      "common": {
                        "id": "4167447279",
                        "name": "Деловой центр",
                        "line_ids": [
                          "100000107"
                        ]
                      },
                      "exits": [
                        {
                          "name": "Деловой центр",
                          "id": "772573685",
                          "position": [
                            37.5377121,
                            55.749150276
                          ],
                          "pickup_point_id": "30574967"
                        }
                      ]
                    },
                    {
                      "transport_types": [
                        "metro"
                      ],
                      "common": {
                        "id": "station__9981061",
                        "name": "Деловой центр",
                        "line_ids": [
                          "2224008691"
                        ]
                      },
                      "exits": [
                        {
                          "name": "Деловой центр",
                          "id": "3103613541",
                          "position": [
                            37.538710074,
                            55.748853854
                          ],
                          "pickup_point_id": "27791285"
                        }
                      ]
                    }
                  ],
                  "pickup_points": [
                    {
                      "id": "32570194",
                      "distance_meters": 1104,
                      "time_seconds": 217,
                      "route_method": "by_car",
                      "position": [
                        37.53331165422808,
                        55.74791991149236
                      ]
                    },
                    {
                      "id": "48382785",
                      "distance_meters": 1034,
                      "time_seconds": 208,
                      "route_method": "by_car",
                      "position": [
                        37.53382794200247,
                        55.74900045310441
                      ]
                    },
                    {
                      "id": "41553621",
                      "distance_meters": 1456,
                      "time_seconds": 263,
                      "route_method": "by_car",
                      "position": [
                        37.5334647316474,
                        55.74783039236024
                      ]
                    },
                    {
                      "id": "42443627",
                      "distance_meters": 1433,
                      "time_seconds": 289,
                      "route_method": "by_car",
                      "position": [
                        37.53594735655815,
                        55.74747695109092
                      ]
                    },
                    {
                      "id": "30574967",
                      "distance_meters": 1324,
                      "time_seconds": 293,
                      "route_method": "by_car",
                      "position": [
                        37.53737152559249,
                        55.749165473015495
                      ]
                    },
                    {
                      "id": "27791285",
                      "distance_meters": 1366,
                      "time_seconds": 308,
                      "route_method": "by_car",
                      "position": [
                        37.537948692971526,
                        55.749349801843046
                      ]
                    }
                  ],
                  "lines": [
                    {
                      "id": "2224008691",
                      "name": "Большая кольцевая линия",
                      "color": "FF29b1a6"
                    },
                    {
                      "id": "100000127",
                      "name": "Филёвская линия",
                      "color": "FF0099cc"
                    },
                    {
                      "id": "1727497101",
                      "name": "Московское центральное кольцо",
                      "color": "FFffa8af"
                    },
                    {
                      "id": "100000107",
                      "name": "Калининско-Солнцевская линия",
                      "color": "FFffdd03"
                    }
                  ]
                }

            parameters:
              - in: header
                name: X-AppMetrica-DeviceId
                type: string
                required: false
              - in: header
                name: X-AppMetrica-UUID
                type: string
                required: false
              - in: header
                name: User-Agent
                type: string
                required: false
              - in: body
                name: body
                required: true
                schema:
                    $ref: "#/definitions/V1StopsNearbyRequest"
            responses:
                "200":
                    description: OK
                    schema:
                        $ref: "#/definitions/V1StopsNearbyResponse"
                "500":
                    description: Internal Server Error
            x-taxi-middlewares:
                api-4.0:
                    pass-not-authorized: true


definitions:

    V1StopsNearbyRequest:
        type: object
        additionalProperties: false
        properties:
            position:
                description: координаты точки для которой делается запрос
                $ref: "persuggest/definitions.yaml#/definitions/Point"
            distance_meters:
                description: предельное расстояние поиска от position
                type: integer
                x-taxi-cpp-type: geometry::Distance
            route_method:
                description: how to calculate the route to PPs
                $ref: "persuggest/definitions.yaml#/definitions/RouteType"
            point_type:
                description: |
                    a или b.
                    планируется для корректировок вроде
                    стоянки для ожидания пассажира
                    и метода расчёта маршрута до точки -
                    пешком или на такси.
                type: string
            transport_types:
                type: array
                description: какой транспорт вернуть в ответе
                items:
                    $ref: "persuggest/definitions.yaml#/definitions/MtTransportType"
            locale:
                description: пользовательская локаль
                type: string
        required:
          - position
          - distance_meters
          - route_method
          - point_type
          - transport_types
          - locale

    V1StopsNearbyResponse:
        type: object
        additionalProperties: false
        properties:
            stops:
                type: array
                items:
                    $ref: "persuggest/definitions.yaml#/definitions/MtStop"
            pickup_points:
                description: all PPs referenced by stops
                type: array
                items:
                    $ref: "persuggest/definitions.yaml#/definitions/MtPickupPoint"
            lines:
                description: all lines referenced by stops
                type: array
                items:
                    $ref: "persuggest/definitions.yaml#/definitions/MtLine"
        required:
          - stops
          - pickup_points
          - lines
```

definitions.yaml:
```yaml
    MtTransportType:
        type: string
        enum:
          - railway
          - metro
          - shuttle
          - bus

    MtLine:
        type: object
        additionalProperties: false
        properties:
            id:
                description: internal unique line id
                type: string
            name:
                type: string
            color:
                description: hex ARGB
                type: string
            number:
                description: |
                    линии метро имеют имя и номер
                    (иногда с буквой, поэтому строка)
                type: string
        required:
          - id
          - name

    MtStop:
        type: object
        additionalProperties: false
        properties:
            transport_types:
                type: array
                items:
                    type: string
                    enum:
                      - metro
                      - bus
                      - railway
                      - shuttle
                      - tramway
            id:
                description: internal unique stop id
                type: string
            name:
                type: string
            line_ids:
                type: array
                items:
                    description: internal unique line id
                    type: string
            exits:
                type: array
                items:
                    type: object
                    additionalProperties: false
                    properties:
                        name:
                            description: имя выхода. может не быть
                            type: string
                        id:
                            description: internal unique exit id
                            type: string
                        position:
                            $ref: "#/definitions/Point"
                        pickup_point_id:
                            type: string
                    required:
                      - id
                      - position
                      - pickup_point_id
        required:
          - transport_types
          - id
          - name
          - line_ids
          - exits

    RouteType:
        type: string
        enum:
          - by_car
          - by_foot

    MtPickupPoint:
        description: |
            best point to pickup for type a
            best point to drop off for type b
        type: object
        additionalProperties: false
        required:
          - id
          - distance_meters
          - time_seconds
          - position
        properties:
            id:
                type: string
            distance_meters:
                description: distance to the nearest PP
                type: integer
                x-taxi-cpp-type: geometry::Distance
            time_seconds:
                description: approx time to the nearest PP
                type: integer
                x-taxi-cpp-type: std::chrono::seconds
            route_method:
                description: how the route to this PP was calculated
                $ref: "#/definitions/RouteType"
            position:
                $ref: "#/definitions/Point"
```
