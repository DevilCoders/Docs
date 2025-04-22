# Интеграция freePasses в YangoWind

Дизайн [тык](https://www.figma.com/file/APbRKVYn8nj6eyBy6aeYxb/Scooter?node-id=249%3A155083)

Изменение внешнего Апи

## `/4.0/scooters/v1/offers/create`
```
OffersCreateResponse:
    type: object
    additionalProperties: false
    required:
        - vehicles
        - offers
        - currency_rules
        - insurance_type
    properties:
        insurance_type:
            type: string
            example: standart
        vehicles:
            type: array
            items:
                $ref: '#/components/schemas/Vehicle'
        currency_rules:
            $ref: '#/components/schemas/CurrencyRules'
        offers:
            type: array
            items:
                $ref: '#/components/schemas/Offer'
        passes: # new
            ref: '#/components/schemas/Passes'

Passes:
    type: object
    description: |
        тут все про пассы
    additionalProperties: false
    properties:
        free_passes:
            $ref: '#/components/schemas/FreePasses'
        super_passes:
            $ref: '#/components/schemas/SuperPasses'

FreePasses:
    type: object
    additionalProperties: false
    required:
        - groups
    properties:
        current:
            $ref: '#/components/schemas/CurrentItem'
        entrypoint:
            $ref: '#/components/schemas/PassEntrypoint'
        groups:
            type: array
            items:
                $ref: '#/components/schemas/GroupPasses'

SuperPasses:
    type: object
    additionalProperties: false
    required:
        - entrypoint
    properties:
        current:
            $ref: '#/components/schemas/CurrentItem'
        entrypoint:
            description: |
                Кнопка для перехода к экрану покупки super pass-ов
            $ref: '#/components/schemas/PassEntrypoint'
        description:
            description: |
                общее описание superpass-ов, я тут немного переживаю за будущее, и думаю
                добавить в PassItem опциональный объект description, с логикой:
                при наличии description у PassItem - он оверайдит общее описание 
            $ref: '#/components/schemas/Description'
        items:
            type: array
            items:
                $ref: '#/components/schemas/PassItem'

PassEntrypoint:
    type: object
    additionalProperties: false
    required:
        - title
    properties:
        title:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
        subtitle:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'

GroupPasses:
    type: object
    additionalProperties: false
    required:
        - group_id
        - items
    properties:
        group_id:
            type: string
            description: идентификатор группы, для ui компоненты Android
        title:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
            description: |
                на основе данного поля рисуется плашка с разделителем и текстом
                если отсутствует - разделителя нет
        subtitle:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
            description: описание свойств группы
        items:
            type: array
            items:
                $ref: '#/components/schemas/PassItem'

CurrentItem:
    type: object
    additionalProperties: false
    required:
        - description
    properties:
        description:
            $ref: '#/components/schemas/Description'
        subscription:
            $ref: '#/components/schemas/Subscription'

PassItem:
    type: object
    additionalProperties: false
    required:
        - type
        - pass_id
        - title
        - is_active
        - is_available
        - is_subscriptable
    properties:
        pass_id:
            type: string
            example: sf_1_hour
        type:
            type: string
            enum:
                - tariff
                - free_pass
                - super_pass
            description: |
                К сожалению, мы вынуждены помержить тариф с пассами
        title:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
        subtitle:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
        price:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
            description: цена в валюте currency_rules, c шаблоном
        purchase_subtitle:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
            description: текст под кнопкой покупки
        is_active:
            type: boolean
            description: |
                Показывает текущий купленый free/super pass
        is_available:
            type: boolean
            description: |
                Показывает доступность freepass-а для покупки, если true - доступен, false - задезейблен
        is_subscriptable:
            type: boolean
            description: |
                Показывает возможность подписаться на автоматическую покупку данного элмента (пока что вседа будет false)
                Вообще, в Wind это делается на клиентах, мы еще не думали как это сделать у нас на бэке

Description:
    type: object
    additionalProperties: false
    required:
        - descriptions
    properties:
        title:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
        subtitle:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
            description: |
                Хотим писать про лимиты, но возможно, стоит вынести в отдельные поля
                subtitle собирать на основе шаблона
        descriptions:
            type: array
            description: описание свойства freePass
            items:
                $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'

Subscription:
    type: object
    additionalProperties: false
    required:
        - renew_info
        - cancellation_info
    properties:
        renew_info: 
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
        cancellation_info:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
```

<details>
<summary markdown="span">example:</summary>

```
{
    "passes": {
        "free_passes": {
            "current": {
                "description": {
                    "title": AttrText, # optional
                    "subtitle": AttrText, # optional
                    "descriptions": [
                        'AttrText'
                    ]
                }
            },
            "entrypoint": {
                "title": AttrText,
                "subtitle": AttrText
            },
            "group": [
                {
                    "title": AttrText,
                    "subtitle": AttrText,
                    "items": [
                        {
                            "type": "tariff",
                            "pass_id": "tariff",
                            "title": AttrText,
                            "subtitle": AttrText,
                            "is_active": true | false, # shows that you have this pass
                            "is_available": true,
                            "is_subscribable": false, # can subscribe or not
                        },
                        {
                            "type": "free_pass",
                            "title": AttrText,
                            "subtitle": AttrText,
                            "is_active": true | false, # shows that you have this pass
                            "is_available": true | false, # is option enabled or disabled
                            "is_subscribable": true | false, # can subscribe or not
                        }
                    ]
                },
                {
                    "title": AttrText,
                    "subtitle": AttrText,
                    "items": [
                        {
                            "title": AttrText,
                            "subtitle": AttrText,
                            "is_active": true | false, # shows that you have this pass
                            "is_available": true | false, # is option enabled or disabled
                            "is_subscribable": true | false, # can subscribe or not
                        }
                    ]
                }
            ],
        },
        "super_passes": {
            "current": {
                "description": {
                    "title": AttrText, # optional
                    "subtitle": AttrText, # optional
                    "items": [
                        'AttrText'
                    ]
                },
                "suvscription": {
                    "renew_info": AttrText,
                    "cancellation_info": AttrText
                }
            },
            "entrypoint": {
                "title": AttrText,
                "subtitle": AttrText,
            },
            "description": {
                "title": AttrText, # optional
                "subtitle": AttrText, # optional
                "items": [
                    'AttrText'
                ]
            },
            "items": [ # тут тоже можно группы, для повтояемости
                {
                    "title": "Month",
                    "subtitle": "Most popular option",
                    "price": "31",
                    "is_active": true | false, # shows that you have this pass
                    "is_available": true | false, # is options enabled or disabled
                    "is_subscribable": true, # can subscribe or not, I offer to skip this functionality right now
                }
            ]
        }
    }
}
```
</details>

## `POST /4.0/scooters/v1/payment/passes`
request
```
PaymentType:
    type: string
    description: Payment method type.
    enum:
        - card
        - applepay
        - googlepay

PaymentMethod:
    type: object
    additionalProperties: false
    required:
        - type
        - id
    properties:
        type:
            $ref: '#/components/schemas/PaymentType'
        id:
            type: string

FreepassPaymentRequest:
    type: object
    additionalProperties: false
    required:
        - free_pass_id
        - payment_method
        - operation_id
    properties:
        pass_id:
            type: string
        operation_id:
            type: string
            description: idempotency-token genereted on client and using for retrying this handler
        payment_method:
            $ref: '#/components/schemas/PaymentMethod'
        subscribe:
            type: boolean
            description: |
                Subscribe user to auto renew this super pass.
                This field will ignore for free passes
```

response 200
```
FreepassPaymentResponse:
    type: object
    additionalProperties: false
    required:
        - operation_id
    properties:
        operation_id:
            type: string
```

### Ошибки
Пока без дезиайнов поэтому что-то примерное

response body 404, 500
```
OperationStatusReason:
    type: object
    additionalProperties: false
    required:
        - code
        - description
    properties:
        code:
            description: reason code
            type: string
        title:
            description: human readable description (internal)
            type: string
        description:
            description: human readable description (internal)
            type: string

StatusResponse:
    type: object
    additionalProperties: false
    required:
      - reason
    properties:
        reason:
            $ref: '#/components/schemas/OperationStatusReason'
```

header for response 429 and 500, используем данный интервал в секундах для следующей попытки
```
headers:
    Retry-After:
        schema:
            type: integer
```

response 409 - возвращаем аутальный operation_id предотвращая паралелльную покупку пассов одного типа
```
StatusResponse:
    type: object
    additionalProperties: false
    required:
      - operation_id
    properties:
        operation_id:
            type: string
```


response 404 - pass_id not found
response 409 - parallel payments, нужно начать полить этот operation_id
response 500 - что-то сломалось, нужно чутка поретраить с дедлайном и с тем же operation_id и перестать

### Параметры запроса
Будем пробовать с клиентским таймаутом 5сек и 3 ретраями в случае 500, на стороне прокси будет 2 попытки по 2400ms


<details>
<summary markdown="span">example:</summary>

request: 
```
{
    "pass_id": "sf_1_hour",
    "operation_id": "298d86798a04401e8a3f7bc39a7c16e6", # uuid4.hex
    "payment_method": {
        "type": "card",
        "id": "somecardid" # from listpaymentmethod
    }
}
```

response:
```
{
    "operation_id": "298d86798a04401e8a3f7bc39a7c16e6"
}
```
</details>

## `GET /4.0/scooters/v1/payment/passes/status?operation_id=<operation_id>`
response 200
```
OperationStatus:
    type: string
    description: status of topup/freepass operation
    enum:
        - pending
        - success
        - failed

OperationStatusReason:
    type: object
    additionalProperties: false
    required:
        - code
        - description
    properties:
        code:
            description: reason code
            type: string
        title:
            description: human readable description (internal)
            type: string
        description:
            description: human readable description (internal)
            type: string

PaymentFreepassStatusResponse:
    type: object
    additionalProperties: false
    required:
      - status
      - reason
    properties:
        status:
            $ref: '#/components/schemas/OperationStatus'
        reason:
            $ref: '#/components/schemas/OperationStatusReason'
```

<details>
<summary markdown="span">example:</summary>

response
```
{
    "status": "failed",
    "reason": {
        "code": "stop",
        "title": "ne smogli",
        "description": "vse ploho, mojno bolshe ne pollit"
    }
}
```
</details>

### Ошибки
header for response 429 and 500, используем данный интервал в секундах для следующей попытки
```
headers:
    Retry-After:
        schema:
            type: integer
```

404 - можно по идеи не обрабатывать, это какой-то корнер кейс, которого не должно происходить


## `DELETE /4.0/scooters/v1/passes/subscription`
Нужно передать заголовок авторизации
response 200 {}
response 500 ошибки смотреть в `POST /4.0/scooters/v1/payment/passes`


### Параметры запроса
Клиентский таймаут: 2сек (возможно мало, и придется подтюнить)
Период между запросами: 1сек, либо из Retry-After

Нужно полить до терминального статуса, который будет гарантировать что операция прошла успешно и пасс выдан пользователю
В случае 500 продолжаем полить игнорируя 500 ответ, считая что платеж в статусе pending

### Логика

- Все изи, в `passes.entrypoint` лежит описание текущего состоянии кнопки покупци опций. На основе `passes.<pass_type>.current`, можно принять решения какие пассы доступны для покупки, если присутсвует `description` - то имеется купленый free пасс
- `free_passes` - самостоятельная структура в которой хранится все необходимое для ее отображения. `groups` - группы free-pass-ов
- `super_passes` - самостоятельная структура в которой хранится все необходимое для ее отображения. `entrypoint` - параметры для кнопки(точка входа на экран покупки суперпассов), `description` - общее описание пассов, `items` - массив суперпассов
- Для покупки freepass-а дергаем `POST /4.0/scooters/v1/payment/passes`, если пятисотит, нужно подергать со старым токеном идемпотентности operation_id, до дедлайна
- Далее полим `GET /4.0/scooters/v1/payment/passes/status?operation_id=<operation_id>` раз в секунду пока не будет успеха
- Оформить подписку можно только на экране super_pass-ов, тогл с подпиской там должен присутствовать всегда. Стейт тогла храним на клиенте
- В зависимости от стейта тогда, отправляем в ручку покупки пассов поле `subscribe: true`
- После успешной покупке супер пасса, при наличии подписки, на экране информации о суперпассе, будет приходить объект `subscription` с текстами, после отмены подписки через ручку `/4.0/scooters/v1/passes/subscription/cancel`, данный объект приходить не будет

## Расчет таймингов

Ручка создание платежа
1. Раундтрип израиль -> yandex dc - 100ms ?
2. Раундтрип yandex dc -> амазон dc - 100ms ?
3. Wind что-то делает у себя - 300ms
4. wind to yandex uid - 100ms
5. last payment method - 100ms
6. create invoce - 100ms

Сумарно: 800ms
Замеры тестинга: 760ms

Будем пробовать с клиентским таймаутом 5сек и 3 ретраями в случае 500, на стороне прокси будет 2 попытки по 2400ms

Ручка поллинга статуса:
1. Раундтрип израиль -> yandex dc - 100ms ?
2. Раундтрип yandex dc -> амазон dc - 100ms ?
3. Wind что-то делает у себя - 50мс (стремимся к 20ms)
4. получаем состояние платежа - 90мс

суммарно
Замеры тестинга: 340ms, и 700ms (плохая логика)


## Ошибки Wind-а при оплате

Ошибки при оплате пассов:
1. ERROR_USER_CAN_ONLY_HAVE_ONE_ACTIVE_FREEPASS - пользователь хочет купить второй фрипасс - это запрещено, можно покупать только второй суперпасс
Как обрабатывать: Наш UI не позволяет выполнить данную операцию, нужно разбираться почему мы разрешили это сделать

2. ERROR_USER_CAN_MOST_HAVE_TWO_SUPER_FREEPASS - при попытке купить больше 2х суперпассов
Как обрабатывать: Наш UI не позволяет выполнить данную операцию, нужно разбираться почему мы разрешили это сделать

3. ERROR_FREEPASS_NOT_EXIST, ERROR_FREE_PASS_NOT_EXIST - передали невалидный pass_id
Как обрабатывать: Не правильная выдача фрипассов с бэка, нужно фексеть бэк асап, бэк будет отдавать 404

4. ERROR_USER_CURRENCY_NOT_MATCH - валюта пользователя (в бэке винда) не совпадает с валютой пасса
Как обрабатывать: ???? Наверное нужно попросить винд вырубить эту проверку

5. ERROR_USER_PURCHASE_FREEPASS_TOO_FREQUENTLY - слишком высокий рейт запросов
Как обрабатывать: Можем сделать 429 с retry-after

6. ERROR_FREE_PASS_CAN_NOT_CHANGE_PACKAGE, ERROR_FREE_PASS_CAN_NOT_CHANGE_TO_FREE_TRIAL - это для фукнционала смены пасса для автопродления
был xxx пасс, можешь поменять на yyy
Как обрабатывать: данный функционал не поддерживается

7. ERROR_PAYMENT_DUPLICATE_TRANSACTION - попытка выполнить транзацию с тем же operation_id
Как обрабатывать: back, вернем 200

8. ERROE_PAYMENT_CREATE_FAILED - ошибка при попытке выполнить платеж на стороне wind->talaria-payments->transactions
Как обрабатывать: 500, и ретраим на клиенте

9. ERROR_USER_ALREADY_HAD_FREE_TRIAL_SUPER_PASS - пользователь хочет купить второй trial pass
Как обрабатывать: Наш UI не позволяет выполнить данную операцию, нужно разбираться почему мы разрешили это сделать


## Особенности

Особенности freePass-а:
1. FreePass и SuperPass имеют разные свойства, но общую схему(нахождусь в процессе выпытывания отличий между ними)
2. В случае если пользователь начал платить за пасс, не дождавшись результата платежа начал поездку, в случае успешной оплаты, freePass должен начать действовать сразу, причем freePass можно купить прям во время поездки, главно это сделать до ее окончания
3. Бэкенд разрешает делать параллельные платежи по разными типам пассов, и запрещает для одного и того же типа пассов


## backend логика хранения статуса платежа

### Зачем?
- Мы не доверяем бэкенду винда, и хотим подстелить соломки в этом месте
- Обрабатывать гонки в случае парралельных платежей
- Иметь больше информации о платежах

1. Заводим таблицу с платежами
2. Заводим stq для поллинга ручки статуса wind-а
3. Меняем логику на слудющую
    1. При успешной оплате делаем запись в базу ставим stq
