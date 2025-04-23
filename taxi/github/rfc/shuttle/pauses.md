# Водительские паузы

## Идея

Находясь на линии водитель может запрашивать перерывы в работе на свои нужды. Каждый такой перерыв - одна пауза.
Их максимальное число и продолжительность задается в сменах. В каждый момент времени на одной смене может выйти не больше
заданного числа водителей.

Когда водитель запрашивает паузу, ему перестают поступать новые заказы и блокируется возможность брать 
пассажиров от борта, но все уже сделанные заказы обязаны быть выполненными. После завершения последнего заказа
непосредственно и начинается пауза, в течение которой ему капают деньги, но заказы не назначаются. 
Когда водитель будет готов выйти на линию, он просит завершить паузу, при этом явным образом не заставляем всегда
уходить с паузы в течение ее установленной продолжительности (потом накажем, если бездельничал сверх нормы).


## Объект паузы в водительском протоколе
TODO

## Водительские ручки

Есть две водительские ручки: запросить паузу и закончить ее.

Ручка запроса паузы имеет вид:
```
/driver/v1/shuttle-control/v1/pause-management/request-pause:
    post:
        description: Запрос паузы водителем
        parameters:
          - name: Accept-Language
            description: Предпочитаемый язык ответа
            in: header
            schema:
                type: string
            required: true
          - name: User-Agent
            in: header
            schema:
                type: string
            required: true
          - name: shuttle_id
            in: query
            required: true
            schema:
                type: string
        responses:
            200:
                description: OK, pause is requested or it has been alread requested
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/ShuttleStatusResponseV2'
            403:
                description: Pause is forbidden to request right now
                content:
                    application/json:
                        schema:
                            $ref: 'shuttle-control/definitions.yaml#/components/schemas/TaximeterError'
            404:
                description: Queried resource is not found
                content:
                    application/json:
                        schema:
                            $ref: 'shuttle-control/definitions.yaml#/components/schemas/TaximeterError'
```

Ручка завершения текущей паузы:
```
/driver/v1/shuttle-control/v1/pause-management/finish-pause:
    post:
        description: Завершение паузы водителем
        parameters:
          - name: Accept-Language
            description: Предпочитаемый язык ответа
            in: header
            schema:
                type: string
            required: true
          - name: User-Agent
            in: header
            schema:
                type: string
            required: true
          - name: shuttle_id
            in: query
            required: true
            schema:
                type: string
          - name: pause_id
            description: pause_id is an idempotency key of the query, not the shuttle_id
            in: query
            required: true
            schema:
                type: string
        responses:
            200:
                description: OK, pause is finished or it has been already over
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/ShuttleStatusResponseV2'
            404:
                description: Queried resource is not found
                content:
                    application/json:
                        schema:
                            $ref: 'shuttle-control/definitions.yaml#/components/schemas/TaximeterError'
```
