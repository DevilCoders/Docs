# Переопределение функционала саммари

## Что хотим

В некоторых случаях существует потребность переопределять функцию кнопки заказа на саммари.
Например, хочется по нажатию на кнопку показывать коммуникацию, если тариф беспилотника сейчас недоступен.
Для тарифа Шаттла при аналогичной ситуации хочется по нажатию на кнопку заказа открывать карточку тарифа, в которой содержится информация о времени работы Шаттла. Сейчас для Шаттла это сделано через клиентский эксперимент, что не очень масштабируемо.

## Что предлагаем

Клиент присылает инфу о том, что поддерживает соответствующий функционал:
```yaml
definitions:
    RoutestatsRequest:
        type: object
        additionalProperties: true
        x-taxi-additional-properties-true-reason: to simplify proxying
        properties:
            supported_features:
                $ref: "#/definitions/SupportedFeatures"

    SupportedFeatures:
        type: array
        items:
            $ref: "#/definitions/SupportedFeature"
        minItems: 1
    
    SupportedFeature:
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
            values:
                type: array
                items:
                    type: string
        required:
          - type
          - values
```

```json
{
  "supported_features": [
    {
      "type": "order_button_actions",
      "values": [
        "open_tariff_card",
        "media",
        "deeplink"
      ]
    }
  ]
}
```

На бэке проверяем поддержку переопределений. Если не поддержаны, то имеем возможность по-старому заблокировать кнопку через `tariff_unavailable`.
Если поддержаны, то в `TariffUnavailable` добавляем поле `action`.
Старые клиенты игнорят это поле и дизейблят кнопку с текстом из `tariff_unavailable.message`.

Новые клиенты при наличии поля используют `ServiceLevel.title`, `ServiceLevel.subtitle` для тайтла, сабтайтла кнопки, вешают на кнопку экшон из поля `action` и раскрашивают кнопку так, как указано в `ServiceLevel.summary_style`, или по умолчанию, как обычно, в желтый.
Отдельно про экшон `expand_summary`: при значении флага `disable_when_expanded=true` и развернутом саммари клиент дизейблит кнопку (кнопка как обычно в таком случае светло серая и некликабельная),
оставляя тайтл и сабтайтл из `ServiceLevel.title`, `ServiceLevel.subtitle`.

```yaml
definitions:
    TariffUnavailable:
        type: object
        additionalProperties: false
        properties:
            code:
                type: string
            message:
                type: string
            order_button_action:
                $ref: "#/definitions/Action"
        required:
          - code
          - message

    Action:
        oneOf:
          - $ref: "#/definitions/TypedDeeplinkAction"
          - $ref: "#/definitions/MediaAction"
          - $ref: "#/definitions/OpenTariffCard"

    TypedDeeplinkAction:
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - deeplink
            deeplink:
                type: string
        required:
          - type
          - deeplink

    MediaAction:
        type: object
        additionalProperties: false
        properties:
            media:
                additionalProperties: false
                type: object
                properties:
                    promo_id:
                        type: string
                required:
                  - promo_id
            prefetch:
                type: string
        required:
          - media

    OpenTariffCard:
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - expand_summary
            disable_when_expanded:
                type: boolean
        required:
          - type
```

Например с безусловным показом медиа
```json
{
  "service_levels": [
    {
      "class": "selfdriving",
      "name": "Беспилотник",
      "is_hidden": false,
      "title": "Беспилотник не работает",
      "tariff_unavailable": {
        "code": "out_of_schedule",
        "message": "Беспилотник не работает",
        "order_button_action": {
          "media": {
            "promo_id": "some_promotion_id"
          }
        } 
      },
      "summary_style": {
        "order_button": {
          "text_color": "#000000",
          "fill": {
            "type": "solid",
            "color": "#F1F0ED"
          }
        }
      }
    }
  ]
}
```

![Example](example_for_sdc.png)


Для удобства клиента берем экшоны в том же виде, что и у шорткатов.
Делать массив экшонов не хочется:
1) сложно придумать ситуацию, когда надо будет сделать множество действий, если заказ сделать всё равно нельзя
2) Если заказ сделать можно, то не хочется давать возможность откладывать показ экрана поиска водителя/курьера, чтобы не беспокоить пользователя
3) в особых случаях, таких как соглашение с условиями перед заказом, уже есть особый механизм, которые это реализует

