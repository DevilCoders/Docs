# API с информацией о дополнительных сборах

## Проблема
Сейчас существует множество полей для получения информации о дополнительных сборах: `charges`, `expenses_holding`, `delivery_fee`, которые для фронтового клиента необходимы только для отрисовки строк с доп. скидкой или с доп. услугой. 
Необходимо определить единый стандарт передачи таких данных с возможностью расширения функционала.

## Решение
В ответе корзины добавить дополнительное поле `additional_payments` рядом с полями `charges` и `expenses_holding`. `additional_payments` будет представлять собой массив из дополнительных платежей.

Структура корзины будет иметь вид:

```
    Cart:
        type: object
        additionalProperties: false
        required:
            ...
            - charges
            - expenses_holding
+           - additional_payments
            ...
        properties:
            ...
            expenses_holding:
                $ref: '#/components/schemas/ExpensesHolding'
            charges:
                description: Дополнительные сборы или платежи, которые ложатся
                    на клиента (доставка, сборка, холдирование и пр.). Основной
                    сбор - это доставка, при этом стоимость доставки может включать
                    в себя стоимость сборки (в этом случае в этом массиве будет
                    присутствовать элемент с типом assembling).
                type: array
                items:
                    $ref: '#/components/schemas/Charge'
+           additional_payments:
+               description: Универсальное поле для дополнительных платежей, 
+                            которые ложатся на клиента.
+               type: array
+               items:
+                   $ref: '#/components/schemas/AdditionalPayment'
            ...
            
```

Структура `AdditionalPayment` универсальна для каждого вида дополнительных платежей и имеет вид:

```
    AdditionalPayment:
        description: Объект, описывающий дополнительные сборы
        type: object
        additionalProperties: false
        required:
            - title
            - amount
            - type
        properties:
            title:
                description: Заголовок
                $ref: '#/components/ColoredText'
            subtitle:
                description: Подзаголовок
                $ref: '#/components/ColoredText'
            amount:
                description: Стоимость дополнительного сбора
                $ref: '#/components/ColoredAmount'
            image_url:
                type: string
                description: url картинки которую надо показать в начале строки
            type:
                description: Тип дополнительного сбора
                type: string
                enum:
                  - delivery_fee
                  - service_fee
                  - assembling_fee
            action:
                $ref: '#/components/schemas/DetailsForm'
```
Поле `type` необходимо для дальнейшего сбора статистики, чтобы определять шторку какого сбора открывал поользователь.
Стоимость является шаблоном для отображения величины сбора, валюты и символа валюты, пока шаблон выглядит так `"20.1 $SIGN$$CURRENCY$"`.

При нажатии на кнопку информации о дополнительном сборе будет появляться структура `DetailsForm`. 
Структуру шторки предлагаю переиспользовать из api плюса, которая приведена ниже:

```
    DetailsForm:
        type: object
        description: Данные для шторки
        required:
            - title
            - description
        additionalProperties: false
        properties:
            title:
                $ref: '#/components/ColoredText'
                description: Заголовок в шторке
            image_url:
                type: string
                description: url картинки которую надо показать
            description:
                $ref: '#/components/ColoredText'
                description: Описание в шторке
            buttons:
                type: object
                description: Кнопки в шторке
                required:
                    - type
                    - buttons
                additionalProperties: false
                properties:
                    type:
                        type: string
                        description: Тип кнопок
                        enum:
                            - block
                            - inline
                    buttons:
                        type: array
                        items:
                            $ref: '#/components/schemas/Button'   
```
Возможна ситуация, что массив кнопок будет пустым. В таком случае никакие кнопки отображаться не будут, будет появляться шторка с информацией и закрыть ее можно будет при помощи смахивания шторки.
```
    Button:
        type: object
        description: Кнопка в шторке
        required:
            - title
            - color
            - id
        additionalProperties: false
        properties:
            title:
                $ref: '#/components/ColoredText'
                description: Текст кнопки
            deeplink:
                type: string
            color:
                $ref: '#/components/ThemedColor'
            id:
                type: string
                description: Идентификатор кнопки (для аналитики)
```
Так как для отрисовки surge необходимо иметь возможность изменять цвет текста и цены, то эти величины описываются структурами:
```
    ColoredAmount:
        type: object
        description: Окрашенная цена
        required:
            - color
            - amount
        properties:
            color:
                $ref: '#/components/ThemedColor'
            amount:
                description: Шаблон, которой сожержит стоимость и плейсхолдеры для поодстановки валюты
                type: string
        additionalProperties: false

    ColoredText:
        type: object
        description: Окрашенный текст
        required:
            - color
            - text
        properties:
            color:
                $ref: '#/components/ThemedColor'
            text:
                type: string
        additionalProperties: false

    ThemedColor:
        type: array
        description: |
            Цвет элемента для разных тем (светлой / темной).
        items:
            type: object
            required:
                - theme
                - value
            additionalProperties: false
            properties:
                theme:
                    $ref: '#/components/Theme'
                value:
                    $ref: '#/components/Color'

    Theme:
        type: string
        description: Цветовая тема приложения (светлая / темная).
        enum:
            - light
            - dark

    Color:
        type: string
        example: '#ffffff'
        description: Цвет элемента.
```

Все тексты для отображения задаются через эесперимент `additional_payments_msg`, если эксперимент не сматчился, то будут приходить дефотные значения для заголовков дополнительных сборов.

Пример того как задаются тексты для эксперимента, приведен ниже:
```
{
  "service_fee": {
    "title": {
      "text": "message.service_fee_title",
      "color": [
        {"theme": "light", "value": "#000000"},
        {"theme": "dark", "value": "#ffffff"}
      ]
    },
    "amount": [
      {"theme": "light", "value": "#000000"},
      {"theme": "dark", "value": "#ffffff"}
    ],
    "action": {
      "title": {
        "text": "message.service_fee_form_title",
        "color": [
          {"theme": "light", "value": "#000000"},
          {"theme": "dark", "value": "#ffffff"}
        ]
      },
      "buttons": [
        {
          "id": "close_button",
          "color": [
            {"theme": "light", "value": "#ffdd55"},
            {"theme": "dark", "value": "#333333"}
          ],
          "title": {
            "text": "message.service_fee_button_close_text",
            "color": [
              {"theme": "light", "value": "#000000"},
              {"theme": "dark", "value": "#ffffff"}
            ]
          }
        },
        {
          "id": "info_button",
          "color": [
            {"theme": "light", "value": "#ffdd55"},
            {"theme": "dark", "value": "#333333"}
          ],
          "title": {
            "text": "message.service_fee_button_info_text",
            "color": [
              {"theme": "light", "value": "#000000"},
              {"theme": "dark", "value": "#ffffff"}
            ]
          },
          "deeplink": "https://more_information/"
        }
      ],
      "description": {
        "text": "message.service_fee_main_text",
        "color": [
          {"theme": "light", "value": "#000000"},
          {"theme": "dark", "value": "#ffffff"}
        ]
      },
      "block_buttons": true
    },
    "subtitle": {
      "text": "message.service_fee_subtitle",
      "color": [
        {"theme": "light", "value": "#000000"},
        {"theme": "dark", "value": "#ffffff"}
      ]
    }
  },
  "delivery_fee": {
    "title": {
      "text": "message.delivery_fee_title",
      "color": [
        {"theme": "light", "value": "#000000"},
        {"theme": "dark", "value": "#ffffff"}
      ]
    },
    "amount": [
      {"theme": "light", "value": "#a500cc"},
      {"theme": "dark", "value": "#a500cc"}
    ],
    "action": {
      "title": {
        "text": "message.delivery_fee_form_title",
        "color": [
          {"theme": "light", "value": "#000000"},
          {"theme": "dark", "value": "#ffffff"}
        ]
      },
      "buttons": [
        {
          "id": "close_button",
          "color": [
            {"theme": "light", "value": "#ffdd55"},
            {"theme": "dark", "value": "#333333"}
          ],
          "title": {
            "text": "message.delivery_fee_button_close_text",
            "color": [
              {"theme": "light", "value": "#000000"},
              {"theme": "dark", "value": "#ffffff"}
            ]
          }
        }
      ],
      "image_url": "image/123delivery.png",
      "description": {
        "text": "message.delivery_fee_main_text",
        "color": [
          {"theme": "light", "value": "#000000"},
          {"theme": "dark", "value": "#ffffff"}
        ]
      },
      "block_buttons": false
    },
    "subtitle": {
      "text": "message.delivery_fee_subtitle",
      "color": [
        {"theme": "light", "value": "#000000"},
        {"theme": "dark", "value": "#ffffff"}
      ]
    },
    "image_url": "https://lightning_picture/"
  }
}
```

### Старые поля
Так как есть необходимость поддерживать старых клиентов, то старые поля сразу удалить нельзя, но необходимо отметить их как `deprecated`. Старые поля, такие как: `charges`, `expenses_holding`, `delivery_fee`, использовать запрещено.

