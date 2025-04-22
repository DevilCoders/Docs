# Отключение случайной скидки при сурже

В скидках в такси есть механизм, который отключает скидку, 
если сурж в тарифе превышает определённое значение (это можно настроить в админке).

Однако, случайные скидки делались через механизм выдачи купонов,
поэтому для них механизма отключения при сурже нет,
что мы и хотим исправить в этой проработке.


### Логика отключения скидки при сурже

Задача: [TAXIBACKEND-34089](https://st.yandex-team.ru/TAXIBACKEND-34089)

Ключевые детали mvp решения описаны в [комментарии](https://st.yandex-team.ru/TAXIBACKEND-34089#6065ca419ba2703c83bdc770),
продублируем их тут:

- Применение купонов в сурж не ограничиваем
- Ручки /status и /roll вызываем в те же моменты, что и раньше, только дополнительно передаём туда координату точки А для расчёта суржа
- При наличии суржа хотим уметь настраивать разные сценарии:
  - отключать игру для пользователя (он вообще ничего не увидит в сурж)
  - ограничить розыгрыш в сурж -- ручка /roll проверит сурж и если он высокий, то не будет разыгрывать купон, а сразу вернёт ответ с неудачным розыгрышем
  - изменить настройки розыгрыша в сурж (например, сильно уменьшить вероятность выигрыша скидки)



### Изменение в экспериментах

Для этого предлагается расширить схему эксперимента `random_discounts` следующими полями
```yaml
        properties:
            surge_settings:
                description: |
                    | Настройки обработки суржа при выдаче случайных скидок
                $ref: '#/definitions/SurgeSettings'

        definitions:
            SurgeSettings:
                type: object
                additionalProperties: false
                description: |
                    | Настройки обработки суржа при выдаче случайных скидок
                required:
                  - max_allowed_surge
                  - surge_policy
                properties:
                    max_allowed_surge:
                        type: number
                        description: |
                            | Максимальное значение суржа в тарифе, при котором скидка будет активна.
                        minimum: 0
                    surge_class:
                        type: string
                        description: |
                            | Если в этом тарифе сурж превысит порог max_allowed_surge, то применится surge_policy.
                            | По умолчанию проверяем сурж по базовому классу суржа __default__ (это econom/uberx)
                            | При указании здесь тарифа (uberx, uberkids, etc) его маппинг в тариф карты суржа 
                            | будет сделан через конфиг TARIFF_CLASSES_MAPPING
                        default: '__default__'
                    surge_policy:
                        type: string
                        enum:
                            - disable
                            - disable-roll
                            - use-surge-discount-settings
                        description: |
                            | Стратегии обработки суржа:
                            | - disable - случайные скидки отключены: ручка /status возвращает disabled, розыгрыш не производится;
                            | - disable-roll - не производим розыгрыш в сурж, а сразу возвращаем ответ, что розыгрыш не был успешен;
                            | - use-surge-discount-settings - используем для розыгрыша скидки в сурж настройки из поля surge_discount_settings.
                    surge_discount_settings:
                        $ref: '#/definitions/DiscountSettings'
```



### Изменение API

В тело запроса ручек `/status` и `/roll` добавляем поле `position`:
```yaml

definitions:
  Point:
    type: array
    description: геокоординаты точки [lon, lat]
    items:
      type: number
      minimum: -180.0
      maximum: 180.0
    minItems: 2
    maxItems: 2
    x-taxi-cpp-type: geometry::Position
    example: "[37.62, 55.75]"

  RandomDiscountStatusRequest:
    type: object
    properties:
      ...
      position:
        $ref: '#/definitions/Point'
        description: Текущее положение пина (точка А)

  RandomDiscountRollRequest:
    properties:
      ...
      position:
        $ref: '#/definitions/Point'
        description: Текущее положение пина (точка А)
```

Логика проверки суржа будет активирована если в эксперименте `random_discounts` задано поле `surge_settings`.
Если при этом в запросе не придёт `position` -- то случайные скидки будут отключены (статус `disabled`).



### Интеграция с суржем 

Для получения значения суржа по геопозиции пользователя 
предлагается использовать кэш `surge-heatmap-cache`.

Пример использования этого кэша: [surge-calculator/v1/get-map-surge](https://github.yandex-team.ru/taxi/uservices/blob/develop/services/surge-calculator/src/views/v1/get-map-surge/get/view.cpp)

Есть две альтернативы:
1. Добавить кэш в сервис
2. Ходить из сервиса в ручку `surge-calculator/v1/get-map-surge`

Лучше использовать кэш, добавив его в свой сервис, так как ручка была сделана для клиентов,
которые не могут добавить кэш к себе в сервис (по комментариям от команды суржа).

Пример значения суржа из кэша (ответ ручки `/v1/get-map-surge`):
```json
{
  "classes": [
    {
      "name": "minivan",
      "value": 0.7241239413770036
    },
    {
      "name": "econom",
      "value": 0.9087666281311189
    },
    {
      "name": "cargo",
      "value": 1.8740523140486363
    },
    {
      "name": "courier",
      "value": 1.5942173646506321
    },
    {
      "name": "comfortplus",
      "value": 0.7272137080607353
    },
    {
      "name": "business",
      "value": 0.7246557087522973
    },
    {
      "name": "__default__",
      "value": 0.908899875683955
    },
    {
      "name": "vip",
      "value": 1.3440128537636022
    }
  ]
}
```

По-умолчанию сурж будем проверять для класса `__default__` (это econom/uberx, в зависимости от зоны).

Для маппинга тарифов убера в тарифы суржа используем конфиг [TARIFF_CLASSES_MAPPING](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/TARIFF_CLASSES_MAPPING).
