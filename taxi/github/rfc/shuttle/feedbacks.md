# Фидбеки на поездки шаттлов

## Получение запроса на фидбек со стороны клиентов

Клиент поллит ручку `/booking/information/` (и в ответе `/booking/cancel/`) для получения статуса заказа, и в терминальном статусе 
(aka `cancelled`/`finished`) отдается поле `feedback` с тайтлом, который зависит от типа отмены заказа, и 
упорядоченным списком вопросов:


```
FeedbackChoice:
    type: object
    additionalProperties: false
    description: Вариант ответа в отзыве
    properties:
        id:
            type: string
            description: идентификатор выбора для бэкенда
        text:
            type: string
            description: текстовое описание варианта
    required:
        - id
        - text

FeedbackInfo:
    type: object
    additionalProperties: false
    description: Экраз отзыва на поездку
    properties:
        title_text:
            type: string
        choices:
            type: array
            items:
                $ref: '#/components/schemas/FeedbackChoice'
    required:
        - title_text
        - choices

...

V1BookingInformation:
    type: object
    additionalProperties: false
    properties:
        booking_id:
            type: string
        status:
            $ref: '#/components/schemas/V1BookingStatus'
        available_actions:
            type: array
            items:
                $ref: '#/components/schemas/V1BookingAvailableAction'
        typed_experiments:
            $ref: '#/components/schemas/V1BookingTypedExperiments'
        shuttle:
            $ref: '#/components/schemas/V1BookingShuttle'
        route:
            $ref: '#/components/schemas/V1BookingRoute'
        ui:
            $ref: '#/components/schemas/V1BookingInformationUi'
        ticket:
            $ref: '#/components/schemas/V1BookingTicketInfo'
        payment:
            $ref: '#/components/schemas/Payment'
        cost:
            $ref: '#/components/schemas/V1BookingCostInfo'
        currency_rules:
            $ref: '#/components/schemas/V1BookingCurrencyRules'
        feedback:
            $ref: '#/components/schemas/FeedbackInfo'
    required:
      - booking_id
      - status
      - available_actions
      - typed_experiments
      - ui
      - route
      - ticket
      - payment
      - cost
      - currency_rules
```

На бэкенде весь список вопросов и настройки экрана (заголовок, нужно ли перемешивать список вопросов, smth else) 
зашит в убер конфиг, который работает по  типам запросов на фидбек: 
`cancelled_by_user`, `cancelled_by_backend` и в будущем `finished`. Максимальная длина отзыва зашита в бэке константой, 
и пока установлено в 500 символов.

## Сохранения фидбека на бэк

Когда пользователь сохраняет фидбек на поездку, вызывается ручка `/feedback/` по аналогии с такси, в которой
происходит вся логика:

```
/4.0/shuttle-control/v1/feedback:
    post:
        x-taxi-middlewares:
            api-4.0: true
        description: Save feedback
        requestBody:
            required: true
            content:
                application/json:
                    schema:
                        $ref: '#/components/schemas/SaveFeedbackRequest'
        responses:
            200:
                description: OK
            400:
                description: Bad request
                content:
                    application/json:
                        schema:
                            $ref: 'shuttle-control/definitions.yaml#/components/schemas/Error'              

components:
    schemas:
        SaveFeedbackRequest:
            type: object
            additionalProperties: false
            properties:
                booking_id:
                    type: string
                choices:
                    type: array
                    description: пункты, которые выбрал пользователь
                    items:
                        type: string
                message:
                    type: string
                    maxLength: 500
                    description: комментарий пользователя
            required:
                - booking_id
                - choices

```
 
Комментарий пользователя опционален (он может не ввести ответ). Бэк ответит 400
при неправильных данных с клиента. Рейтинг пока не передается в фидбек, т.к. 
в первой итерации работаем только с отменами, и для них оценки нет.

