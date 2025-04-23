# Система Быстрых Платежей (СБП)

## Задача

Поддержать оплату заказов Такси с помощью СБП

## Доработки API

### 3.0/zoneinfo

В `payment_options` добавляется ключ `sbp`: true.

### 3.0/paymentmethods

```yaml
    sbp:
        $ref: '#/definitions/SBPPaymentMethod'
    service_token:
        type: string
    
    definitions:
        SBPPaymentMethod:
            type: object
            additionalProperties: false
            required:
                - payment_available
            properties:
                payment_available:
                    type: boolean
        
```

Пример:
```json
{
    "service_token": "some token",
    "sbp": {
        "payment_available": true
    }
}
```


### 3.0/routestats

```yaml
    payment:
        oneOf:
            - $ref: '#/definitions/SBPPayment'
    
    definitions:
        SBPPayment:
            type: object
            additionalProperties: false
            required:
                - type
            properties:
                type:
                    type: string
                    enum:
                        - sbp
```

```json
{
    "payment": {
        "type": "sbp"
    }
}
```

### 3.0/orderdraft

```yaml
    payment:
        oneOf:
            - $ref: '#/definitions/SBPPayment'
    
    definitions:
        SBPPayment:
            type: object
            additionalProperties: false
            required:
                - type
            properties:
                type:
                    type: string
                    enum:
                        - sbp
```

```json
{
    "payment": {
        "type": "sbp"
    }
}
```


### 3.0/taxiontheway

```yaml
    sbp_widget:
        type: object
        additionalProperties: false
        required:
            - text
            - payment_button
            - purchase_token
            - service_token
            - user_email
        properties:
            icon_tag:
                type: string
            text:
                $ref: '#/definitions/Text'
            payment_button:
                $ref: '#/definitions/PaymentButton'
            deadline_timestamp:
                type: integer
            purchase_token:
                type: string
            service_token:
                type: string
            user_email:
                type: string
    notifications:
        top_notifications:
            type: array
            items:
                $ref: '#/definitions/TopNotification'
    definitions:
        Text:
            type: object
            additionalProperties: false
            required:
                - title
                - loading_title
            properties:
                title:
                    type: string
                loading_title:
                    type: string
        PaymentButton:
            type: object
            additionalProperties: false
            required:
                - text
            properties:
                text:
                    type: string
                background_color:
                    type: string
        TopNotification:
            type: object
            required:
                - id
                - text
                - icon_tag
            properties:
                id:
                    type: string
                text:
                    type: string
                icon_tag:
                    type: string


```

Пример:

```json
{
    "sbp_widget": {
        "icon_tag": "some image tag",
        "text": {
            "title": "Оплатить через приложение банка", 
            "loding_title": "Проверяем оплату" 
        },
        "payment_button": {
            "text": "Оплатить $TIME$", 
            "background_color": "bgMain"
        },
        "deadline_timestamp": 123123,
        "purchase_token": "123", 
        "service_token": "123", 

        "user_email": "foo@example.com"
    },
    "notifications": {
        "top_notifications": [
            {
                "id": "uuid", 
                "text": "Оплата прошла", 
                "icon_tag": "some image tag" 
            }
        ]
    }
}
```

`user_email` - костыль для PaymentSDK. В PaymentSDK email пользователя необязателен, но тем не менее без него сейчас ничего не работает. По существу он нужен, чтобы отправлять чеки, однако в Такси чеки можно смотреть в истории заказов, а большинство пользователей email не имеют.

Поэтому, чтобы не блокироваться о доработки PaymentSDK, добавляем обязательное поле `user_email`. Обязательное потому, что даже если в новых версиях PaymentSDK нам оно больше не понадобится, всё равно придётся отправлять его для старых клиентов. Чтобы не ошибиться, сделаем обязательным.

### Семантика отображения доступности метода оплаты на клиенте

Если метода оплаты нет нигде, метод оплаты не отображается.
Если метода оплаты нет в ответе `3.0/zoneinfo`, но есть в `3.0/paymentmethods`, метод оплаты отображается как недоступный.
Если метод оплаты есть в ответе `3.0/zoneinfo`, но его нет в `3.0/paymentmethods`, метод оплаты не отображается.

Если `zoneinfo.payment_options.sbp == true && paymentmethods.sbp.payment_available == true`, то метод считается доступным и с его помощью можно создать заказ.

Если `zoneinfo.payment_options.sbp == false && paymentmethods.sbp.payment_available == true`, то метод считается недоступным, однако отображается.

Если `zoneinfo.payment_options.sbp == true && paymentmethods.sbp.payment_available == false`, метод оплаты не отображается.

Если `zoneinfo.payment_options.sbp == false && paymentmethods.sbp.payment_available == false`  метод оплаты не отображается.
