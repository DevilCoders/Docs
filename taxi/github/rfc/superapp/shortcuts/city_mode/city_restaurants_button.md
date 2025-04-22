# Кнопка "Еда с собой" в шоркатах

## Задача
Добавить кнопку в шорткаты режима "Город", при нажатии на которую открывается режим с ресторанами на карте

![Screenshot](static/city_restaurants_button.png)

## Предложение
Предлагается расширить существующий экшен `discovery` новым `mode='restaurants'`

### Запрос
В запросе `v1/products/screen/city-mode` для `DiscoverySupportedAction` добавляется `mode='restaurants'`

```yaml
DiscoverySupportedAction:
    type: object
    additionalProperties: false
    required:
        - type
        - modes
    properties:
        type:
            type: string
            enum:
                - discovery
        modes:
            type: array
            items:
                type: string
                enum:
                    - masstransit
                    - drive
                    - scooters
                    - restaurants
```
Пример:
```json
{
	"state": {},
	"shortcuts": {
        ...
		"supported_actions": [{
			"type": "discovery",
			"modes": ["drive", "masstransit", "scooters", "restaurants"]
		}],
        ...
	},
	"position": [37.497465818585269, 55.776581649175299],
}
```

### Ответ
Для `TypedDiscoveryAction` добавляется `mode='restaurants'`
При открытии карты с помощью этого экшена layers_context прокидывается в /layers для управления типов ресторанов, которые нужно показать на карте
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
                enum:
                    - masstransit
                    - drive
                    - scooters
                    - restaurants
            layers_context:
                type: object
                additionalProperties: true
                x-taxi-additional-properties-true-reason: |
                    дополнительный контекст для хождения в layers (например,
                    нужны только остановки метро, нужны только легковые
                    машины драйва, только рестораны с самовывозом)
        required:
          - mode
          - type
```
