# Ручки запросов недавних позиций

Мы предоставляем ручки для запроса позиций для контракторов. Это ручки
/position
/bulk/positions
/shorttrack
/bulk/shorttracks
/subscribe/positions  - это стриминг, в случае grpc или long-polling

Балковые ручки - это просто одиночные ручки куда можно послать запросы сразу по нескольким водителям.

Все ручки возвращают один тип ответа, вот его схема

{% cut 'Схема' %}
```yaml
PositionsForContractor:
    description: An object with an array of positions for each requested source
    type: object
    properties:
        contractor:
            $ref: "#/components/schemas/ContractorId"
    additionalProperties:
        type: array
        items:
            $ref: "fts-universal-signal/definitions.yaml#/definitions/UniversalSignal"
    required:
      - contractor
PositionsResponse:
    description: An array with positions for each contractor and each source
        for the contractor
    type: array
    items:
        $ref: "#/components/schemas/PositionsForContractor"
```
{% endcut %}

Вот пример ответа любой из ручек

```yaml
contractor:
  uuid: u1
  dbid: db1
Verified: 
  - timestamp: 1649970983056
    source: "Android"
    transport_type: "Scooter"
    region: "spb"
    geodata:
      - time_shift: 0
        positions:
          - position: [52.569089, 39.60258]
            accuracy: 5
            speed: 16.6
            direction: 125
  - timestamp: 1649970982056
    source: "Android"
    transport_type: "Scooter"
    region: "spb"
    geodata:
      - time_shift: 0
        positions:
          - position: [52.569084, 39.60257]
            accuracy: 5
            speed: 16.6
            direction: 125
AndroidGps:
  - timestamp: 1649970983056
    source: "Android"
    transport_type: "Scooter"
    region: "spb"
    geodata:
      - time_shift: 0
        positions:
          - position: [52.569089, 39.60258]
            accuracy: 5
            speed: 16.6
            direction: 125
  - timestamp: 1649970982056
    source: "Android"
    transport_type: "Scooter"
    region: "spb"
    geodata:
      - time_shift: 0
        positions:
          - position: [52.569084, 39.60257]
            accuracy: 5
            speed: 16.6
            direction: 125
```

### Актуальные позиции

Ручка /position возвращает самую актуальную позицию водителя на данный момент.

{% cut 'Схема ручки' %}

```yaml
/v1/legacy/position:
    post:
        description: Returns various positions as requested by user.
        parameters:
          - in: query
            name: pipeline
            description: Pipeline from which the position should be returned.
            required: true
            schema:
                type: string
          - in: query
            name: uuid
            description: Contractor UUID.
            required: true
            schema:
                $ref: "driver-id/definitions.yaml#/definitions/ContractorId"
          - in: query
            name: max_age
            type: integer

          - in: query
            name: sources
            type: array
            items:
              type: string

        requestBody:
        responses:
            '200':
                description: Success
                content:
                    application/json:
                        schema:
                            $ref: '../definitions.yaml#/components/schemas/PositionsResponse'

```


Нас интересуют две схемы отсюда: схема запроса и схема ответа. Схема запроса выглядит вот так:

{% endcut %}

Вот примеры запросов в эту ручку

Дай мне позицию этого водителя
**v1/taxi/position?uuid=u1&dbid=db1&sources=Verified**

Дай мне позицию этого водителя не старее чем 5 секунд
**v1/taxi/position?uuid=u1&dbid=db1&max_age=5&sources=Verified**

Дай мне позицию этого водителя не старее чем 5 секунд, хочу источники Verified и
AndroidGps
**v1/taxi/position?uuid=u1&dbid=db1&max_age=5&sources=Verified,AndroidGps**

Вот так мог бы выглядеть ответ:
```yaml
contractor:
  uuid: u1
  dbid: db1
Verified: 
  - timestamp: 1649970983056
    source: "Android"
    transport_type: "Scooter"
    region: "spb"
    geodata:
      - time_shift: 0
        positions:
          - position: [52.569089, 39.60258]
            accuracy: 5
            speed: 16.6
            direction: 125
  - timestamp: 1649970982056
    source: "Android"
    transport_type: "Scooter"
    region: "spb"
    geodata:
      - time_shift: 0
        positions:
          - position: [52.569084, 39.60257]
            accuracy: 5
            speed: 16.6
            direction: 125
AndroidGps
  - timestamp: 1649970983056
    source: "Android"
    transport_type: "Scooter"
    region: "spb"
    geodata:
      - time_shift: 0
        positions:
          - position: [52.569089, 39.60258]
            accuracy: 5
            speed: 16.6
            direction: 125
  - timestamp: 1649970982056
    source: "Android"
    transport_type: "Scooter"
    region: "spb"
    geodata:
      - time_shift: 0
        positions:
          - position: [52.569084, 39.60257]
            accuracy: 5
            speed: 16.6
            direction: 125
```



Разберем по шагам что есть что. Самые простые параметры - это max_age и sources.
* max_age ограничивает максимальную глубину по времени, за которую мы будем смотреть.
* sources указывает какие источники сигналов брать.

### Шорттреки

Ручка /shorttrack похожа ручку /position, но возвращает отрезок последних точек.

{% cut 'Схема' %}

```yaml
paths:
    /v1/shorttrack:
        post:
            description: Returns shorttrack for requested driver
            parameters:
              - in: query
                name: pipeline
                description: Pipeline from which the position should be returned.
                required: true
                schema:
                    type: string
              - in: query
                name: uuid
                description: Contractor UUID.
                required: true
                schema:
                    $ref: "driver-id/definitions.yaml#/definitions/ContractorId"
              - in:query
                name: max_age:
                description: Maximum age of the coordinate (in seconds). By default
                    - +inf.
                type: integer
                x-taxi-cpp-type: std::chrono::seconds
                minimum: 0
              - in:query
                name: sources:
                $ref: "#/components/schemas/SignalSources"
              - in: query
                name: num_positions:
                description: Maximum number of position in short track. If not
                    set, all available positions are returned.
                type: integer
                x-taxi-cpp-type: std::uint32_t
                minimum: 1

            responses:
                '200':
                    description: Success
                    content:
                        application/json:
                            schema:
                                $ref: '../definitions.yaml#/components/schemas/PositionsResponse'
                '400':
                    description: Ill-formed request
```


{% endcut %}

Примеры запросов:

Дай мне весь шорттрек этого водителя
**v1/taxi/position?uuid=u1&dbid=db1**
```yaml
sources:
 - Verified
```

Дай мне ту часть шорттрека этого водителя, которая не старше 5 секунд
**v1/taxi/position?uuid=u1&dbid=db1**
```yaml
sources:
 - Verified
max_age: 5
```

Дай мне ту часть шорттрека этого водителя, которая не старше 5 секунд, 
возьми данные указанных источников, и для каждого источника не более чем 7
позиций в шорттреке
**v1/taxi/position?uuid=u1&dbid=db1**
```yaml
sources:
 - Verified
max_age: 5
num_positions: 7
```

### Балковые ручки

Балковые ручки отличаются просто добавлением параметра contractor_ids в котором передаются id'шники контракторов.
```yaml
BulkRequestExtention:
    description: Additional properties required for bulk requests
    type: object
    additionalProperties: true
    x-taxi-additional-properties-true-reason: for allOf
    properties:
        contractor_ids:
            description: An array of contractor ids.
            type: array
            minItems: 1
            items:
                $ref: "#/components/schemas/ContractorId"
    required:
      - contractor_ids
```

Добавился параметр num_positions, ограничивающий длину шорттрека и пропал параметр algorithm, т.к. он становится бесмысленным (критерии для ретраев получаются либо настолько узкими что никогда не будут тригерится, либо бесмысленными).

**Сценарии которые решаем**
1. Сценарий Еды/Лавки. Когда курьер приближается к месту назначения, Еда запрашивает три его источника (Verified, Gps, Lbs) и если хотя бы один из них около места назначения, то ему разрешают нажать "на месте". При этом Еда использет алгоритм WithRetry т.к. ей важно получить позицию.
2. Сценарий логина: Логину очень нужна позиция водителя. Так же, он знает что за моменты до его вызова, позиция была отправленна в бек и она там где-то есть. Логин тоже использует алгоритм WithRetry с достаточно большими ретраями.
3. Сценарий диспатча - диспатч хочет получать все альтернативы для самой актуальной позиции, но не хочет ждать. Он использует алгоритм AsOfNow и указывает в alternatives_selector ```all```
4. Сценарий аналитиков и куска диспатча: Аналитики для анализов хотят видеть позиции и шорттреки притянутые на X1...XN секунд, где X1..XN - параметр запроса. При этом они не хотят угадывать какие именно X доступны. Т.е. если у нас есть prediction_for = 10, 20, 30, а они передают X=15, то надо округлить его в сторону ближайшего предсказания и вернуть.
   TODO: @laxader как такое будем решать?
5. Сценарий протокола: Протоколу нужна последняя позиция источника Verified и последняя притянутая.

### Ручки запроса треков

Ручка запроса трека умеет возвращать данные контрактора за указанный промежуток
времени.

{% cut 'Схема' %}

```yaml
paths:
    /v1/{pipeline}/track:
        post:
            description: Returns historical track for requested driver
            parameters:
              - in: path
                name: pipeline
                description: Pipeline from which the position should be returned.
                required: true
                schema:
                    type: string
              - in: query
                name: uuid
                description: Contractor UUID.
                required: true
                schema:
                    $ref: "driver-id/definitions.yaml#/definitions/ContractorUuid"
              - in: query
                name: dbid
                description: Optional contractor DBID.
                required: false
                schema:
                    $ref: "driver-id/definitions.yaml#/definitions/ContractorDbid"

            requestBody:
                description: Body
                required: true
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/TrackRequest'
            responses:
                '200':
                    description: Success
                    content:
                        application/json:
                            schema:
                                $ref: '../definitions.yaml#/components/schemas/PositionsResponse'

```

```yaml
TrackRequest:
    description: Describes requested track
    type: object
    additionalProperties: false
    properties:
        sources:
            $ref: "../definitions.yaml#/components/schemas/SignalSources"
        from_time:
            type: string
            format: date-time
            description: Start interval timestamp.
        to_time:
            type: string
            format: date-time
            description: End interval timestamp.
        processing:
            $ref: "#/components/schemas/TrackProcessing"

TrackProcessing:
    description: Describes pre- and postprocessing of the track
    type: object
    additionalProperties: false
    properties:
        simplify:
            type: object
            additionalProperties: false
            properties:
                enable:
                    type: boolean
                    description: Enable simplification algorithms for track
                        preprocessing.
            required:
              - enable

        adjust:
            type: object
            additionalProperties: false
            properties:
                enable:
                    type: boolean
                    description: Postprocess track by adjusting it to the
                        road graph.
            required:
              - enable

        filter:
            type: object
            additionalProperties: false
            properties:
                enable:
                    type: boolean
                    description: Enable filtering algorithms for track preprocessing.
            required:
              - enable
```

{% endcut %}

Вот примеры запросов

Простой запрос - дай все что есть с полночи до 10 для этого водителя
**v1/taxi/track?uuid=u1&dbid=db1**
```yaml
sources:
 - Verified
from_time:'2022-01-01T00:00:00Z'
to_time:'2022-01-01T10:00:00Z'
```

Мы позволяем сделать некоторую постобработку прямо на нашей стороне, например
попросить притянуть трек
**v1/taxi/track?uuid=u1&dbid=db1**
```yaml
sources:
 - Verified
from_time: '2022-01-01T00:00:00Z'
to_time: '2022-01-01T10:00:00Z'
processing:
  adjust: True
```

Или сделать медианную фильтрацию
**v1/taxi/track?uuid=u1&dbid=db1**
```yaml
sources:
 - Verified
from_time: '2022-01-01T00:00:00Z'
to_time: '2022-01-01T10:00:00Z'
processing:
  simplify: True
```

