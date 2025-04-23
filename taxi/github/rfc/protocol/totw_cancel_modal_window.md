# Модалка для отменённых заказов
## Проблема

В https://st.yandex-team.ru/TAXIA-7887 была добавлена возможность кастомизировать экран отмены заказа. В рамках данного rfc хочется решить следующие проблемы:
- предоставить возможность направлять пользователя на произвольные экраны приложения нажатием на кнопку на модалке
- позволить кастомизировать модалку не только на `expired`-заказах, но и на `cancelled` тоже.
- причесать API, поскольку API из задачи выше явно зашивает поведение кнопок в названия ключей для надписей на них.

## Дизайн

![Дизайн](./img/cancel_modal_window.png)

## Предложение по API

### 3.0/taxiontheway

```yaml
# ...
    notifications:
        type: object
        additionalProperties: false
        properties:
            order_status_window:
                $ref: '#/definitions/OrderStatusWindow'
    
definitions:
    OrderStatusWindow:
        type: object
        additionalProperties: false
        required:
            - title
            - text
            - reason
            - main_button
        properties:
            title:
                type: string
            text:
                type: string
            reason:
                type: string
                description: Причина отображения модалки. Нужна в первую очередь для клиентской  аналитики.
                examples:
                  - 'early_hold_cancel'
                  - 'antifraud_cancel'
                  - 'search_expire'
            main_button:
                $ref: '#/definitions/Button'
            extra_button:
                $ref: '#/definitions/Button'
    Button:
        type: object
        additionalProperties: false
        required:
            - text
            - color
            - action
        properties:
            text:
                type: string
            color:
                type: string
                example: 'buttonMain'
            text_color: # if null, textOnControl will be used
                type: string
                example: 'textMain'
            action:
                oneOf:
                    - $ref: '#/definitions/TypedGoToScreenAction'
                    - $ref: '#/definitions/TypedDeeplinkAction'
                    - $ref: '#/definitions/TypedRepeatOrderAction'
    TypedGoToScreenAction:
        type: object
        additionalProperties: false
        required:
            - type
            - screen
        properties:
            type:
                type: string
                enum:
                    - go_to_screen
            screen:
                type: string
                enum:
                    - summary
                    - payment_methods
                    - current_order_payment_methods
    TypedDeeplinkAction:
        type: object
        additionalProperties: false
        required:
          - deeplink
          - type
        properties:
            deeplink:
                type: string
            type:
                type: string
                enum:
                  - deeplink
    TypedRepeatOrderAction:
        type: object
        additionalProperties: false
        required:
          - type
        properties:
            type:
                type: string
                enum:
                  - repeat_order
    TypedDoNothingAction:
        type: object
        additionalProperties: false
        required:
          - type
        properties:
            type:
                type: string
                enum:
                  - do_nothing
```

Пример ответа:
```json
{
    "notifications": {
        "order_status_window": {
            "title": "Поездку отменили - оплата не прошла",
            "text": "Мы не смогли заморозить деньги на карте. Проверьте, что с ней всё в порядке или измените способ оплаты на наличные",
            "reason": "early_hold_cancel",
            "main_button": {
                "text": "К способам оплаты",
                "color": "buttonMain",
                "text_color": "textMain",
                "action": {
                    "type": "go_to_screen",
                    "screen": "payment_methods"
                }
            }
        }
    }
}
```

Договариваемся, что клиент поддерживает отображение такой модалки в любой ситуации, а бек понимает, в каком статусе такая модалка может быть полезна. Также договариваемся, что при наличии двух кнопок `main_button` всегда снизу.

### Доступные экшены

- `go_to_screen` — переходит к нужному экрану (определяется с помощью `"screen"`)
  - `summary` — завершает поездку и открывает саммари для создания нового заказа
  - `payment_methods` — завершает поездку и открывает выбор способа оплаты и саммари
  - `current_order_payment_methods` — открывает выбор способа оплаты, не завершая поездку
- `deeplink` — завершает поездку и открвыает диплинк
- `repeat_order` — завершает поездку и повторяет заказ
- `do_nothing` — просто скрывает алерт