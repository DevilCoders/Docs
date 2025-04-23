### Описание

Предлагается в ответ routestats
в поле alternatives.options[].service_levels[].combo_order.alert_properties
добавить новое поле fake_passengers_number_selector, которое будет требовать
от клиента показать интерфейс для указания количества пассажиров.

#### Что нужно решить в момент написания этого RFC

При выборе комбо-тарифа попросить пользователя указать количество пассажиров.
Диапазон выбираемого числа пассажиров задаётся в ответе routestats.
Также задаётся допустимый диапазон количества пассажиров,
с которым можно продолжить оформление заказа.

#### Структура

```yaml
AlertProperties:
    type: object
    properties:
        icon_tag:
            type: string
        title:
            type: string
        subtitle:
            type: string
        text:
            type: string
        lower_text:
            type: string
        decline_button_text:
            type: string
        confirm_button_text:
            type: string

        ### NEW ###
        fake_passengers_number_selector:
            $ref: FakePassengersNumberSelector

FakePassengersNumberSelector:
    additionalProperties: false
    properties:
        selector_max_number:
          type: integer
        max_allowed_number:
          type: integer
        error_text_too_many_passengers:
          type: string
```
