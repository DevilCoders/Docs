####  Ручка входных позиций

Ручка принимает на вход пользовательские сигналы. Ничего особенного в ней нет.
Сигналы принимаются в любом количестве, но надо понимать что большинство сервисов не умеют двигать время назад и смешивать их. Ожидается что сигналы доходят до системы в пределах 3-5 минут.

Пример входящего запроса

**/v2/position/store?pipeline=taxi&uuid=abcde**
```yaml
 - timestamp: 1649970983056
   source: "Verified"
   transport_type: "car"
   region: "moscow"
   geodata:
       position: [52.569089, 39.60258]
       accuracy: 5
       speed: 16.6
       direction: 125
```
Здесь pipeline - taxi, uuid - abcde, dbid опущен

{% cut 'Схема запроса' %}
```yaml
    /v2/position/store:
        post:
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                          type: object
                          additionalProperties: false
                          required:
                            - positions
                          properties:
                              positions:
                                  type: array
                                  items:
                                      $ref: '#/definitions/IncomingSignal'

            description: Сохранить координату в пайплайне `pipeline`

            parameters:
              - in: query
                name: pipeline
                description: Name of pipeline
                required: true
                schema:
                    type: string
              # Мы передаем их в query ради быстрой отладки по access-логам
              - in: query
                name: uuid
                required: true
                type:
                  $ref: "#/definitions/ContractorId"

            responses:
                200:
                    description: OK
                400:
                    description: Некорректные параметры запроса
                    content:
                        application/json:
                            schema:
                                $ref: '../definitions.yaml#/definitions/PostError'
                401:
                    description: Не авторизован
                404:
                    description: Неизвестный пайплайн
                500:
                    description: Внутренняя ошибка
```

{% endcut %}
