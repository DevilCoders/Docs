# История нотификаций по тегам

## Проблема:

Нужно уметь получать историю нотификаций по тегам, которые могут представлять собой: номер заказа, один из айдишников пользователя или любую другую информацию, известную на момент отправки, по которой хотелось бы получать историю.

1. Нужно уметь получать в момент отправки уведомления данные тегов
2. Нужно сохранять теги, связывая их с историей
3. Нужно валидировать теги, чтобы не было разных тегов с одинаковой семантикой
4. Нужно уметь отличать теги, которые содержат чувствительные данные
5. Нужно уметь возвращать историю по тегам

## Решение:

### Получение тегов:

Теги будем получать в боди ручки отправки нотификации. Для этого расширим его полем `tags`.

```yaml
tags:
    description: |
        Теги для поиска нотификаций. Валидируются через такси конфиг EATS_NOTIFICATIONS_HISTORY_TAGS
    type: array
    items:
        type: object
        additionalProperties: false
        properties:
            key:
                type: string
            value:
                type: string
        required:
            - key
            - value
```

### Валидация тегов:

Мы не хотим давать возможность пользователям сервиса создавать произвольные теги:
1. Это может привести к тому, что мы не будем знать, какие данные хранятся под какими ключами и потенциально можем пропустить чувствительные данные в тегах.
2. Могут появляться разные теги с одной семантикой, например, order_nr === order_id.

Для этого заводим taxi-config, который будет содержать все допустимые теги и при этом делить их на две группы: с чувствительными данными и без.

Схема:
```yaml
default:
    regular: []
    sensitive: []
maintainers: [airmyxa, tabota]
tags: [notfallback]
description: Список тегов, которые можно использовать для получения истории нотификаций
schema:
    type: object
    additionalProperties: false
    properties:
        regular:
            description: Теги, в которых нет чувствительных данных
            type: array
            items:
                type: string
        sensitive:
            description: Теги, в которых есть чувствительные данные
            type: array
            items:
                type: string

```

При получении тегов в ручке отправки уведомления мы не будем использовать те теги из запроса, которых нет во множестве тегов в такси конфиге.

В дальнейшем можно будет продумать вариант оповещения клиента о том, что он прислал невалидный тег.

### Сохранение тегов:

Теги будем сохранять в отдельной табличке в таком формате:
`[tag_key, tag_value, notification_token, updated_at]`.

Для поиска по тегам нужно будет добавить индексы.

По табличке нужно будет обязательно настроить архивацию по полю `updated_at`. 


### Получение истории по тегам:

Для получения истории нотификаций по тегам делаем отдельную ручку:

```yaml
    /v1/notification/get-history-by-tags:
        post:
            description: Возвращает историю уведомлений
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
                            required:
                                - tags
                            properties:
                                tags:
                                    description: Список тегов, по которым нужна история. 
                                    type: object
                                    additionalProperties:
                                        type: string
            responses:
                200:
                    description: История уведомлений
                    content:
                        applications/json:
                            schema:
                                type: object
                                additionalProperties: false
                                required:
                                    - notifications
                                properties:
                                    notifications:
                                        type: array
                                        items:
                                            type: object
                                            additionalProperties: false
                                            properties:
                                                notification:
                                                    $ref: '../definitions.yaml#components/schemas/NotificationHistory'
                                                tags:
                                                    type: array
                                                    items: 
                                                        type: object
                                                        additionalProperties: false
                                                        properties:
                                                            key:
                                                                type: string
                                                            value:
                                                                type: string
                                                        required:
                                                            - key
                                                            - value
                                            required:
                                                - notification
                                                - tags
                                required:
                                    - notifications
```