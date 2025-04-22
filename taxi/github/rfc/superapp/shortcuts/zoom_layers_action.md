# Шорткат отзума на объекты слоёв на карте

## Что хотим?

На экране дискавери Шаттла появилось желание завести в шторе шорткат, по нажатию на которой
на клиенте происходит отзум на маршруты Шаттлов.

## Как сделаем?

Добавляем такой вот экшон:

```yaml
    ZoomLayersFeatureAction:
        description: zoom on some layers features
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - zoom_layers_feature
            payload:
                oneOf:
                  - $ref: "#/definitions/ZoomLayersFeatureMode"
                discriminator:
                    propertyName: mode
                    mapping:
                        all_object_types: "#/definitions/ZoomLayersFeatureMode"
        required:
          - type
          - payload

    ZoomLayersFeatureMode:
        description: zoom on all features with object type from `object_types`
        type: object
        additionalProperties: false
        properties:
            mode:
                type: string
                enum:
                  - all_object_types
            object_types:
                type: array
                items:
                    type: string
                minItems: 1
        required:
          - mode
          - object_types
```

Шорткат целиком:
```json
{
  "title": "Где маршруты?",
  "shortcut_id": "some_id",
  "type": "action-driven",
  "width": 3,
  "height": 3,
  "background": {
    "color": "#ABCABC"
  },
  "action": {
    "type": "zoom_layers_feature",
    "payload": {
      "mode": "all_object_types",
      "object_types": [
        "shuttle_route"
      ]
    }
  }
}
```

## Что делаем на клиенте?

На экране дискавери Шаттла:
1. Отправляем на бэк в `supported_actions` инфу о поддержке нового экшона и моды для него
(см. ниже).
2. Поддерживаем на экране дискавери Шаттла новый экшон. По нажатию зумимся на все фичи с типом,
который присутствует в `object_types`.

*Важно:* на всякий случай проверить, что на остальных экранах (особенно на главном) на бэк
не отправляется инфа о поддержке нового экшона отзума.

## Что делаем на бэке?

Добавляем в ручке шторы дискавери Шаттла обработку нового экшона.

Парсим в `supported_actions` новое значение:
```json
{
  "supported_actions": [
    {
      "type": "zoom_layers_feature",
      "modes": [
        "all_object_types"
      ]
    }
  ]
}
```
