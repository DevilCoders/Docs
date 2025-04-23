# Барабаны Reloaded в Сити

**Что хочется:** иметь отдельные барабаны на разные тарифы на разные тарифы.
При смене тарифа хочется, чтобы клиент перезапросил finalsuggest и получил
другие барабаны в ответе. Помимо этого хочется иметь возможность указывать
некие настройки отображения для барабанов.  
**Проблема:** нет возможности заставить клиент делать запрос finalsuggest заново
при изменении состояния. `should_redirect`, который есть в схеме ответа по
пикап-поинтам, нынче Android-клиентом игнорируется (а iOS?), так что предлагается
выработать новую, более современную схему. Для барабанов же нет возможности
кастомизировать тайтл/сабтайтл, размер барабана

## Предлагаемое решение

### Кастомизация барабана

Для барабанов надо показывать тайтл/сабтайтл. Предлагается добавить их как
AttributedText. Также возможно имеет смысл указывать число выборов, видимых
в барабане и размер текста у выборов.

```yaml
PositionChoices:
    description: информация для 'барабанов'
    type: object
    additionalProperties: false
    properties:
        choices:
            type: array
            items:
                $ref: '#/definitions/PositionChoice'
        selected_choice_id:
            description: id выбранного терминала
            type: string
        selected_point_id:
            description: id выбранного выхода
            type: string
        title:
            $ref: '#/definitions/AttributedText'
        subtitle:
            $ref: '#/definitions/AttributedText'
        visible_choices_count:
            description: Сколько нужно показывать в барабане за раз.
                Нечетное число. Например 3 или 5
            type: integer
            default: 3
        font_size:
            description: Размер текста у чойсов в барабане
            type: integer
        choice_padding:
            description: Сколько в dp должно быть паддинга вокруг текста с чойсом
            type: number
    required:
      - choices
      - selected_choice_id
      - selected_point_id
```

### Повторный запрос finalsuggest по смене тарифа

Предлагается сделать такой новый экшен:
```yaml
RepeatRequestAction:
    type: object
    description: Говорит клиенту о необходимости заново сходить в /finalsuggest
        для актуализации ответа с обновленными параметрами в запросе. Условия
        задаются в immediate_actions (например, если сменился тариф).
        При этом routestats передергиваться не должен, если не точка в ответе осталась той же
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - repeat_request
    required:
      - type
```

А также добавить новый триггер `tariff_change` в `V1FinalsuggestResponse.condition_actions`.
Но в существующей схеме указать список валидных тарифов рядом с условием нельзя, поэтому
сделаем `V1FinalsuggestResponse.conditional_actions_v2`. Параллельно предлагаю расширить
условия с `OneOf(List[String])` до `AllOf(OneOf(List[Action]))`.

А также добавить новый триггер `tariff_change` в `V1FinalsuggestResponse.condition_actions`:
```yaml
V1FinalsuggestResponse:
    type: object
    additionalProperties: false
    properties:
        results:
            # ...
        points:
            # ...
        # ...
        conditional_actions_v2:
            description: Действия, которые должны быть выполнены по условию (v2)
            type: array
            items:
                $ref: '#/definitions/ConditionalActionV2'
        condition_actions:
            # Старый депрекейтим, хотя и возвращаем тут действия,
            # которые могут быть представлены одним только типом

ToTaxiCondition:
    description: Выполняется, когда пользователь идет по флоу такси
        (выбирает шоткат такси или нажимает на кнопку выбора т. B)
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - to_taxi
    required:
      - type

ChangeToUnwhitelistedTariffCondition:
    description: Выполняется при смене тарифа на тот, который не перечислен в `tariff_whitelist`
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - change_to_unwhitelisted_tariff
        tariff_whitelist:
            type: array
            items:
                type: string
    required:
      - type
      - tariff_whitelist

ActionCondition:
    oneOf:
      - $ref: '#/definitions/ToTaxiCondition'
      - $ref: '#/definitions/ChangeToUnwhitelistedTariffCondition'
    discriminator:
        propertyName: type
        mapping:
            to_taxi: '#/definitions/ToTaxiCondition'
            change_to_unwhitelisted_tariff: '#/definitions/ChangeToUnwhitelistedTariffCondition'

ActionConditionsOneOf:
    type: array
    items:
        $ref: '#/definitions/ActionCondition'

ActionConditionsOneOfAllOf:
    description: |
        `[[a, b], [c, d], [e, f]]` значит `(a AND b) OR (c AND d) OR (e AND f)`
    type: array
    items:
        $ref: '#/definitions/ActionConditionsOneOf'

ConditionalActionV2:
    type: object
    additionalProperties: false
    properties:
        conditions:
            $ref: '#/definitions/ActionConditionsOneOfAllOf'
        actions:
            type: array
            items:
                oneOf:
                    - $ref: "persuggest/definitions.yaml#/definitions/ShowPopupAction"
                    - $ref: "persuggest/definitions.yaml#/definitions/PullOutOfZoneAction"
                    - $ref: "persuggest/definitions.yaml#/definitions/RepeatRequestAction"
    required:
        - conditions
        - actions
```

Ниже расписано на примере.

### Предполагаемое взаимодействие

Для старых клиентов реализуем старую логику барабанов на главном тоже. Новым же делаем новый флоу:

1. При пин-дропе внутрь зоны идет запрос с `state.current_mode = "main"`, с бэка возвращается
   conditional action по `to_taxi` - `PullOutOfZoneAction` без барабанов
    ```json5
    {
      "action": "pin_drop",
      "geo_tap": false,
      "position": [
        37.538574157280806,
        55.74714680771294
        // ^ позиция где-то внутри башни
      ],
      "state": {
        // ...
        "current_mode": "main",  // <- барабанов не будет
        "selected_class": "comfortplus"
      },
      // ...
    }
    ```

    ```json5
    {
      "results": [
        // обычный результат по едовой логике
      ],
      // position_choices не будет
      // ...
      "conditional_actions_v2": [
        {
          "actions": [
            {
              "type": "pull_out_of_zone"
            }
          ],
          // oneOf([allOf([to_taxi])]) = to_taxi
          "conditions": [
            [
              {
                "type": "to_taxi"
              }
            ]
          ]
        }
      ],
      "condition_actions": [
        // Здесь для старых клиентов дублируется то, что получается представить в виде строк
        {
          "actions": [
            {
              "type": "pull_out_of_zone"
            }
          ],
          "conditions": [
            // В новом формате тут только type, так что представить можем
            "to_taxi"
          ]
        }
      ]
    }
    ```
2. При переходе в таксишный сценарий происходит перезапрос с `state.current_mode = ""`
   (от `PullOutOfZoneAction`). Бэк при этом теперь уже показывает барабан и тянет точку к
   барабанному пикап-поинту. Дополнительно возвращается conditional action с вайтлистом тарифов.
    ```json5
    {
      "action": "pin_drop",
      "geo_tap": false,
      "position": [
        37.538574157280806,
        55.74714680771294
      ],
      "state": {
        // ...
        "current_mode": "",  // <- таксишный сценарий, будут барабаны в ответе
        "selected_class": "comfortplus"  // <- барабаны будут соответствовать этому тарифу
      },
      // ...
    }
    ```
   Ответ см. ниже.
3. При смене тарифа на тот, которого в этом вайтлисте нет, нужно перезапросить finalsuggest
   с актуальной информацией в запросе. Запрос аналогичен п.2, за исключением филдов, тарифа,
   еще чего-то, что могло с тех пор измениться. Ответ также аналогичный. Барабаны будут
   соответствовать уже новому тарифу. Также в conditional actions придет список тарифов, на
   которых валиден уже этот ответ
4. По запросу на не-премиальный тариф будет возвращаться вайтлист с не-премиальными тарифами
   и наоборот: для премиального - премиальные тарифы. Так, перезапрос будет делаться в том
   случае, когда меняется категория тарифа, а при смене между Экономом и Комфортом - делаться
   не будет.

Пример полного ответа с шага 2:
```json5
{
  "results": [
    {
      "point_id": "moscow_city_point_t15",
      "lang": "ru",
      "log": "ytpp://МоскваСити/moscow_city_point_t15",
      "method": "np_zone_pickuppoint",
      "position": [
        37.53888687094915,
        55.750326031735185
      ],
      "subtitle": {
        "text": "Москва, Россия",
        "hl": []
      },
      "text": "Россия, Москва, Москва Сити, Меркурий Сити - Т15",
      "title": {
        "text": "Москва Сити, Меркурий Сити - Т15",
        "hl": []
      },
      "uri": "ytpp://МоскваСити/moscow_city_point_t15",
      "type": "address",
      "city": "Москва",
      "street": "1-й Красногвардейский проезд",
      "house": "15",
      "postal_code": "123112"
    },
    /* ... */
  ],
  "zones": { /*...*/ },
  "position_choices": {
    "choices": [
      {
        "id": "moscow_city",
        "name": "Москва Сити",
        "points": [
          {
            "id": "moscow_city_point_t1",
            "name": "Эволюция - Т1"
          },
          /* ... */
        ]
      }
    ],
    "selected_choice_id": "moscow_city",
    "selected_point_id": "moscow_city_point_t15",
    "title": {
      "items": [
        {
          "type": "text",
          "font_weight": "bold",
          "font_size": 32,
          "text": "Крутите новый барабан!"
        }
      ]
    },
    "subtitle": {
      "items": [
        {
          "type": "text",
          "text": "Точки посадки на Ultima немного другие. Придется изменить место посадки"
        }
      ]
    }
  },
  "points": [
    {
      "type": "pickuppoint",
      "id": "moscow_city_point_t15",
      "geometry": [
        37.53888687094915,
        55.750326031735185
      ],
      "name": "Меркурий Сити - Т15",
      "uri": "ytpp://МоскваСити/moscow_city_point_t15"
    },
    /* ... */
  ],
  "points_icon_image_tag": "custom_pp_icon_black_test",
  "typed_experiments": { /*...*/ },
  "services": {
    "taxi": {
      "available": true,
      "nearest_zone": "moscow"
    }
  },
  "conditional_actions_v2": [
    {
      "actions": [
        {
          // Делаем перезапрос за новым барабаном ...
          "type": "repeat_request"
        }
      ],
      "conditions": [
        [
          {
            // ... если тариф сменили на что-то кроме Эконома и К+
            "type": "change_to_unwhitelisted_tariff",
            "tariff_whitelist": [
              "econom",
              "comfortlus"
            ]
          }
        ]
      ]
    }
  ],
  "condition_actions": [
    // Пусто, т.к. change_to_unwhitelisted_tariff тут задать не получится
  ]
}

```
