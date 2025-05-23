## Бизнес задача

### Описание

В главную штору Go смотрят мало людей — её вытягивают порядка 10% DAU. Шторе не хватает функциональных блоков, к ней стоит относиться как к пульту управления СуперАппом.

Так же разделение шторы на функциональные части с более узким функционалом, позволит разделить виджеты между командами. И сделать эти виджеты действительно автономными 

<p float="left">
  <img src="./static/SuperWidgetEats.jpg" width="width:33%" />
  <img src="./static/SuperWidgetMarket.jpg" width="width:33%" /> 
  <img src="./static/SuperWidgetOrders.jpg" width="width:33%" />
</p>

### Задача

Добавить в штору кастомизируемый набор виджетов.

## Решение 

`Backend Driven UI` - Хорошо решает задачу с витриной, но может быть не практичен для функциональной технологии виджетов.
Так как виджеты должны быть автономными и выполнять свои внутренние запросы при необходимости, обновлять UI в зависимости от стейта и действий пользователя

Было принято решение делать виджеты самостоятельными и заложить на клиентах возможность их встраивания не только в штору шорткатов.

Все виджеты будут объединять 3 параметра `id`,`type` и `payload`. 
`type` - Служит для определения клиентом какой именно виджет им необходимо отобразить
`id` - Идентификатор для того, чтобы переиспользовать одинаковые виджеты с разными целями. Например, отобразить несколько виджетов заказов разбив их по сервисам. Так же идентификатор можно будет передавать при запросах виджета, чтобы бекенд понимал какую информацию предоставить.
 
`payload` - Дополнительные параметры виджета. В зависимости от реализации каждого виджета поля могут быть обязательными и нет. 

**JSON:**
```JavaScript
{
    "type": "new_shiny_widget",
    "id": "123456",
    "payload": {
        ...
    }
}

```

**YAML**
```yaml
Widget:
    type: object
    additionalProperties: false 
    required:
        - id
        - type
    properties:
        id:
            type: string
        type:
            type: string
        payload:
            $ref: '#WidgetPayload'

WidgetPayload:
    oneOf:
    - $ref: 
```

В запрос отправляем `screen` и `orders` для полного контекста

**Запрос:**
```JavaScript
{
    "screen_type": "multiorder",
    "orders_info": [
       {
        "order_id": "123",
        "service": "eats",
        "waypoints": [
            {
                "type": "A",
                "latitude": 43.2220
                "longitude": 76.8512
            },
            {
                "type": "B",
                "latitude": 51.1605
                "longitude": 71.4704
            }
        ]
       }
    ],
    "supported_widgets": [
        "new_shiny_widget",
        ...
    ]
}

```

### Контейнеры для виджетов

Структура виджетов не должна меняться в не зависимости от мест, где они приходят 

Сейчас, по дизайну в [Figma](https://www.figma.com/file/DunX6incgxkvFRWgLZhoST/🕹-Главный-экран?node-id=1741%3A54000), реализуем виджеты:
- Поверх шторы в мультизаказе
- Поверх WebView EatsKit 
- Поверх Нативной шторы

**JSON:**
```JavaScript
{
    "widgets":[ 
        {
            "type": "new_shiny_widget",
            "id": "123456",
            "payload": {}
        },
         ...
    ],
```

## Виджеты

- [orders_widgets](./orders_widgets.md)

