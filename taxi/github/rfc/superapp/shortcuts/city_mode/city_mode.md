# Режим "В городе"

## Задача

Уметь переходить в особый режим, в котором на карте отображается несколько разных типов объектов (самокаты, автомобили Драйва, остановки общественного транспорта и т.д.). Уметь в этом режиме отображать небольшой разводящий экран, по которому можно уйти в конкретный режим самокатов/драйва/т.п. См. также дизайн ниже.

<details><summary>Картинки</summary>
![Режим](./static/v_gorode_screen.png)
</details>

## Предложение

### Новый action

Добавляем новый action следующего вида:
#### Вариант 1 (отклоняем)
```yaml
TypedCityModeAction:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - city_mode
        mode:
            type: string
            example: city
        layers_context:
            type: object
            additionalProperties:
                type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: |
                    дополнительный контекст для хождения в layers (например,
                    нужны только остановки метро или нужны только легковые
                    машины драйва)
    required:
      - mode
      - type
```

Пример:
```json
{
    "type": "city_mode",
    "mode": "city",
    "layers_context": {
        "scooters": {
            "charged": true
        },
        "drive": {
            "class": "fixprice"
        }
    }
}
```

Плюсы:
- можно использовать существующую ручку почти не изменяя API
Минусы:
- вводится новый "синтетический" `mode`
- как следствие предыдущего пункта: сложно переиспользовать для других целей
- меняется семантика `context`: раньше это были данные только одного `mode`, сейчас надо из ключей выковыривать `mode`, из значений контексты и как-то их рассовывать.

#### Вариант 2 (выбираем)
```yaml
TypedCityModeAction:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - city_mode
        mode:
            type: string
            example: city
        layers_context:
            type: object
            additionalProperties: false
            required:
                - type
                - objects
            properties:
                type:
                    type: string
                    enum:
                        - multi
                objects:
                    type: array
                    items:
                        oneOf:
                            - $ref: "#/definitions/DriveFixpointOffersContext"
                            - $ref: "#/definitions/OrgGeosearchContext"
                            - $ref: "#/definitions/MasstransitContext"
                        discriminator:
                            propertyName: type
                            mapping:
                                drive_fixpoint_offers: "#/definitions/DriveFixpointOffersContext"
                                org_geosearch: "#/definitions/OrgGeosearchContext"
                                masstransit: "#/definitions/MasstransitContext"
                                                        
    required:
      - mode
      - type
```

Примеры:

С контекстом
```json
{
    "type": "city_mode",
    "layers_context": {
        "type": "multi",
        "objects": [
            {
                "type": "scooters",
                "charged": true
            },
            {
                "type": "drive_fixpoint_offers",
                "class": "fixprice"
            }
        ]
    },
    "mode": "city"
}
```

Без контекста
```json
{
    "type": "city_mode",
    "mode": "city"
}
```

Плюсы по сравнению с вариантом 1:
- можно задавать спецификацию объектов внутри массива `layers_context` через строгие схемы с `enum` для `mode`, что удобнее парсить

#### Вариант 3 (отклоняем)
```yaml
TypedCityModeAction:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - city_mode
        layers:
            type: array
            items:
                type: object
                required:
                    - mode
                    - layers_context
                properties:
                    mode:
                        type: string
                        example: drive
                    layers_context:
                        type: object
                        additionalProperties:
                            type: object
                            additionalProperties: true
                            x-taxi-additional-properties-true-reason: |
                                дополнительный контекст для хождения в layers (например,
                                нужны только остановки метро или нужны только легковые
                                машины драйва)

    required:
      - type
      - layers
```

Пример:
```json
{
    "type": "city_mode",
    "layers": [
        {
            "mode": "scooters",
            "layers_context": {
                "charged": true
            }
        },
        {
            "mode": "drive",
            "layers_context": {
                "class": "fixprice"
            }
        }
    ]
}
```

Плюсы:
- Гибче, можно переиспользовать для других задач.
- Данные и `mode` неразрывно связаны.
- Сохраняется структура объектов, содержащий `mode` и контекст.
Минусы:
- Меняется API, нужно писать новую ручку в `layers`.

При обработке этого `action` клиент запрашивает (по-видимому, параллельно) ручку `screens` с `screen_name`=`city_mode` (т.е. по url `4.0/mlutp/v1/products/screens/city_mode`; см. [rfc про экраны шорткатов](../multiple_screens/multiple_screens.md)) и ручку `layers` (какую именно, определимся здесь после выбора из вариантов выше).
### Точка входа в режим "В городе"

В ответе `products` в объекте `modes[mode=taxi]` появляется новое поле `top_screen_objects` со следующей схемой:
```yaml
top_screen_objects:
  type: array
  items:
    oneOf:
      - type: object
        additionalProperties: false
        required:
            - type
            - id
            - title
            - action
        properties:
            type:
                type: string
                enum:
                  - round_button
            id:
                type: string
            title:
                $ref: '#/components/schemas/AttributedText'
            action:
              oneOf:
                - $ref: '#/components/schemas/TypedDeeplinkAction'
                - $ref: '#/components/schemas/TypedDiscoveryAction'
                - $ref: '#/components/schemas/TypedCityModeAction'
            align:
              type: string
              # enum:
              #   - left
              #   - right
```

Клиент должен кешировать полученные кнопки и отображать их до тех пор, пока не получит ответ ручки `products`. Если предыдущего ответа `products` не было (свежая установка) - кнопка не отображается. 

При отсутствии необязательного поля `align` кнопки выравниваются по левому краю.

Предусматривается возможность переходить в режим города как из самой кнопки "В город" (для этого ей нужно будет присвоить соответствующее название, например "Самокаты"), так и из кнопки на шторе, которая откроется по нажатию на кнопку "В город". Так или иначе, такую возможность предоставит уже реализованный `TypedDiscoveryAction`.

Дополнительно: `image_tag` для кнопки режима "В городе" (4 стрелочки) (скажем, `superapp_city_mode_icon`), а также иконку самокатов (`superapp_scooters_icon`) следует зашить в клиент для того, чтобы отображать, если скачать image_tag не удалось.

### Индикация клиентской поддержки
#### Для action

Для индикации клиентской поддержики для `action` режима города клиент отправляет в `supported_actions` объект следующего вида:

```yaml
CityModeSupportedAction:
    type: object
    additionalProperties: false
    required:
        - type
        - modes
    properties:
        type:
            type: string
            enum:
                - city_mode
        modes:
            type: array
            items:
                type: string
                enum:
                    - masstransit
                    - drive
                    - scooters
```

Пример:
```json
{
    "supported_actions": [
        {
            "type": "city_mode",
            "modes": [
                "masstransit",
                "drive",
                "scooters"
            ]
        }
    ]
}
```


#### Для `top_screen_objects`

Индикация клиентской поддержки не вводится: клиенты, которые не умеют их отображать, просто не обработают это поле.


## План работ

https://st.yandex-team.ru/TAXIBACKEND-34838