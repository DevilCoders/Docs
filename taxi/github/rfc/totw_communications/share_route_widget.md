## Задача

Отображать виджет, по нажатию на который можно отправить маршрут другому человеку.

## Дизайн


![image](static/share_route_example.jpg)

## API

Добавляем новый `action` - `share_route_button`. Тогда получить интерфейс, требуемый в дизайне, можно будет с помощью виджета `actions_arrow_button`, см. пример.

```yaml
    Action:
        oneOf:
          # ...
          - $ref: "#/definitions/ShareRouteButtonAction"
    
    ShareRouteButtonAction:
        type: object
        additionalProperties: false
        required:
            - type
        properties:
            type:
                type: string
                enum:
                    - share_route_button
```
## Пример

```json{
    "promotions": {
        "promoblocks": {
            "items": [
                {
                    "id": "some_promoblock_id",
                    "display_on": [
                        "totw"
                    ],
                    "title": {
                        "items": [
                            {
                                "type": "text",
                                "text": "Отправить маршрут близкому"
                            }
                        ]
                    },
                    "text": {
                        "items": [
                            {
                                "type": "text",
                                "text": "Он получит смс с деталями поездки"
                            }
                        ]
                    },
                    "icon": {
                        "image_tag": "some_tag"
                    },
                    "widgets": {
                        "actions_arrow_button": {
                            "items": [],
                            "color": "#ABABAB",
                            "actions": [
                                {
                                    "type": "share_route_button"
                                }
                            ]
                        }
                    }
                }
            ]
        }
    }
}
```