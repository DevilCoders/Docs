## Задача
Продумать кнопки для перехода в режим дискавери (транспорт, драйв) 

![Турбокнопки](https://jing.yandex-team.ru/files/privet/Untitled%202.d509c93.png)


## Расширение клиентского API

*Примечание: описание предполагает расширения ручки products из RFC турбокнопок 
https://github.yandex-team.ru/taxi/rfc/pull/440*


Добавляем новый тип действия `"type": "discovery"` для кнопок и кирпичиков. 
```json
{
    "action": {
        "type": "discovery",
        "mode": "masstransit",
        "layers_context": {
          "type": "some_context_type",
          "param_1": "xxxx",
          "param_2": "yyyy"
        }
    }
}
```

По этому действию должен быть выполнен переход на экран с картой. На этом 
экране приложение должно ходить в ручку `/4.0/layers/v2/objects` с:
* `state.screen = discovery` 
* `state.mode = action.mode`
* `context = action.layers_context` 

#### Схема действия `discovery`
```yaml
TypedDiscoveryAction:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - discovery
        mode:
            type: string
            example: masstransit
        layers_context:
            type: object
            descripton: | 
              дополнительный контекст для хождения в layers (например, нужны только 
              остановки метро или нужны только легковые машины драйва)
            additionalProperties: true
     required:
        - type
        - mode
```

Если приложение поддерживает действие `discovery` и включен эксперимент `map_objects_layer`, то в запросе ручки 
`/4.0/mlutp/v1/products` нужно указать:

```json
{
    ...
    "supported_actions": [
        ...
        {"type": "discovery", "modes":  ["masstransit", "drive"]}
    ],
    ...
}
```
`modes` - список поддерживаемых режимов.

#### Недоступность ручки /4.0/layers/v2/objects
При недоступности сервиса layers в режиме дискавери не будет объектов на карте.
По-хорошему нужно это как-то обрабатывать. 
Не стоит переходить на экран дискавери, пока мы не получили первый ответ от 
ручки /4.0/layers/v2/objects. 

Если нет ответа от /4.0/layers/v2/objects, то клиент должен 
ретраить с экспоненциальным таймаутом:

T = min(2 ^ (M - 1), 16) секунд. То есть:
1 сек, 2 сек, 4 сек, 8 сек, 16 сек, 16 сек, ...

Если в течение 10 секунд не было ответа, то нужно написать сообщение 
об ошибке "Режим транспорта недоступен".

## Реализация кнопок с режимом `discovery` на бэкенде [на будущее]

Для MVP можно добавлять кнопки в сервисе `shortcuts` через третий эксперимент, 
но в будущем скорее всего понадобятся более сложные логики. 

Например, общественный транспорт мы умеем только в России или Драйв мы умеем 
только в Москве, Спб и Казани. Или, например, кнопку Драйва мы отображаем только для 
пользователей, зарегистрированных в Драйве.

Предлагается сделать ручку `/4.0/layers/v1/discovery-buttons` в сервисе `layers`, 
которая будет возвращать список дискавери-кнопок, которые нужно добавить в 
ответ ручки `products`.

Формат запроса:
```json
{
  "user_context": {
    "bbox": [
      35.8962177956883,
      56.81290553670576,
      35.90024110921064,
      56.808980333875304
    ],
    "pin_position": [
      35.897940886390266,
      56.81144027116202
    ],
    "show_at": "2020-01-01T00:00:00+00:00",
    "supported_modes": ["masstransit", "drive"]
  }
}
```


*Вопрос*: хотим ли мы делать шорткаты для переходов в режим транспорта? 
Если хотим, то нужна более общая ручка, которая просто скажет, можно ли перейти 
в такой-то режим дискавери или нет. 

Формат ответа (v1/products):
```json
{
    "buttons": [
        {
            "id": "some-unique-id",
            "title": "Транспорт",
            "icon_tag": "masstransit_icon_tag",
            "background": { "color": "#D9D4BE" },
            "text_style": { "color": "#000000" },
            "overlays": {
                "shape": "label",
                "background": {"...": "..."},
                "attributed_text": {"items": []}
            },
            "action": {
                "type": "discovery",
                "mode": "masstransit"
            }
        }
    ],
     "header": [
        {
            "shortcut_id": "some-unique-id",
            "title": "Транспорт",
            "icon_tag": "masstransit_icon_tag",
            "background": { "color": "#D9D4BE" },
            "text_style": { "color": "#000000" },
            "overlays": {
                "shape": "label",
                "background": {"...": "..."},
                "attributed_text": {"items": []}
            },
            "action": {
                "type": "discovery",
                "mode": "masstransit"
            },
            "width": 2,
            "height": 1,
            "type": "header-action-driven",
            "service": "masstransit"
        }
    ]

}
```
* вводится новый тип `header-action-driven` для кирпичиков, в action'e которых
есть поле type. Сделано это для того, чтобы поддержать TypedAction'ы, введенные
для `discovery`-кнопок
* для получения `discovery`-кирпичиков нужно указать тип `header-action-driven` в
секции `supported-features` (см. файл products.md)
* в `action.type` должно быть значение из `supported_actions`, 
приходящих от клиента

## Реализация кирпичиков с типом `discovery` на бэкенде
На данный момент кирпичики и кнопки имеют разные API. Есть 2 способа 
реализовать кирпичики Драйва и Транспорта:

- **Введение "новых" кирпичиков** [принято]:  
    Сейчас action'ы кирпичиков и кнопок отличаются наличием поля "type" в
    action'e. Если добавить это поле в action кирпичиков (т. е. добавить поддержку
    TypedAction'ов для кирпичиков), то можно будет переиспользовать логику
    формирования кнопок типа `discovery`. Минусы: разделение кирпичиков на
    "старые" и "новые".
   
- **Поддержка существующей структуры** [отклонено]:  
    Поддержка разделения action'ов кирпичиков (без типа) и кнопок (с типом).
    Минусы: большое дублирование кода на бэкенде, т. к. для 
    `discovery`-кирпичиков action'ы будут различными.
    
    ```yaml
    DiscoveryAction: # для кирпичиков
        type: object
        additionalProperties: false
        properties:
            mode:
                type: string
                example: masstransit
            layers_context:
                type: object
                descripton: | 
                  дополнительный контекст для хождения в layers (например, нужны только 
                  остановки метро или нужны только легковые машины драйва)
                additionalProperties: true
         required:
            - mode
    ```
