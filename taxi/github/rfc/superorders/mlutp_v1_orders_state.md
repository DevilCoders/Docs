# Ручка управлению поллингом заказов в супераппе

![схема](https://jing.yandex-team.ru/files/ulturgashev/order-state-launch.jpg "scheme")

## Архитектура

Ручки `mlutp/v1/orders/state` и `v1/orders/state` находятся в сервисе `order-state`

### Текущий вариант(x2 запросов в `order-state`):
Из `3.0/launch` выполяняются 2 параллельных запросов в `order-core/active-orders` и `order-state/v1/eats/orders/state` после этого, полученые данные передаются в `order-state/v1/orders/state` для формирования 

### Вероятный вариант(вероятно, этап 2, так как будет необходимо перекроить весь api-proxy/3.0/launch):
`order-state/v1/orders/state` - самостоятельно делает запросы в `order-core/active-orders` и `order-state/v1/eats/orders/state` и передаёт флаги успешности запросов.

## API

`order-state/mlutp/v1/orders/state` - внешняя ручка для управления состоянием поллинга

- request
```(json)
{
    "known_orders": [
        {
            "orderid":"order1",
            "status":"driving",
            "tags": {
                "taxiontheway": "1590674415"
            },
            "force": true,
            "service": "taxi"
        },
        {
            "orderid":"order1",
            "status":"delivering",
            "tags": {
                "eats_tracking": "1590674415"
            },
            "force": false,
            "service": "eats"
        }
    ],
    "tags": {
        "eats": "encoded_tags",
        "grocery": "encoded_tags",
        "taxi": "encoded_tags"
    }
}
```



- response:
```(json)
{
    "orders": [
        {
            "orderid": "order_1",
            "service": "taxi",
            "status": "driving", # в этапе 1 данный статус возвращается тот же, что нам прислали клиенты
            "need_request": ["taxiontheway"],
            "tags": {
                "taxiontheway": "1590674416"
            },
            "update_status": "actual"
        },
        {
            "orderid": "order_1",
            "service": "eats",
            "status": "some_status",
            "need_request": ["eats_tracking"],
            "tags": {
                "eats_tracking": "1590674416"
            },
            "update_status": "stale"
        }
    ],
    "allowed_changes": [
        {
            "service": "taxi",
            "can_make_more_orders": true
        },
        {
            "service": "eats",
            "can_make_more_orders": false,
            "no_more_orders_reason": "reason"
        }
    ]
    "tags": {
        "eats": "encoded_tags",
        "grocery": "encoded_tags",
        "taxi": "encoded_tags"
    }
}
```


`order-state/v1/orders/state` - внутренняя ручка для launch

`3.0/launch`

### Изменения в launch

- request
```(json)
{
    ...
    "supported_services": ["taxi","eats","grocery","etc..."],
    "known_orders": [
        {
            "orderid": "order1",
            "tags": {
                "fast_info": "encoded_tags",
                "part2": "encoded_tags"
            },
            "service": "taxi",
            "status": "driving"
        },
        {
            "orderid":"order1",
            "tags": {
                "full_info": "encoded_tag"
            },
            "service": "eats",
            "status": "cooking",
            "some_field": "some_value"
        }
    ]
}
```

- response
```(json)
{
    ...
    "mlutp_orders_state": {
        "tags": {
            "eats": "encoded_tags",
            "grocery": "encoded_tags",
            "taxi": "encoded_tags"
        },
        "orders":[
            {
                "orderid": "order_1",
                "service": "taxi",
                "status": "driving",
                "tags": {
                    "fast_info": "encoded_tag",
                    "part2": "encoded_tag"
                },
                "need_request": ["fast_info", "part2"],
                "update_status": "actual"
            },
            {
                "orderid": "order_1",
                "service": "eats",
                "status": "cooking",
                "some_field": "some_value",
                "tags": {
                    "full_info": "encoded_tag"
                },
                "need_request": [],
                "update_status": "stale"
            }
        ],
        "allowed_changes": [
            {
                "service": "taxi",
                "can_make_more_orders": true
            },
            {
                "service": "eats",
                "can_make_more_orders": false,
                "no_more_orders_reason": "reason"
            }
        ],
        "polling_policy": [
            {
                "service": "taxi",
                "part_name": "fast_info",
                "url": "/4.0/taxi/order/fast",
                "fields": ["field1", "field2", "field3"],
                "polling_type": "tag_defined",
                "part_type": "totw",
                "priority": 2,
                "required": true
            },
            {
                "service": "taxi",
                "part_name": "part2",
                "url": "/4.0/part2",
                "fields": ["field1", "field2", "field3"],
                "polling_type": "tag_defined",
                "part_type": "totw",
                "priority": 3
            },
            {
                "service": "taxi",
                "part_name": "route",
                "url": "/4.0/taxiroute",
                "fields": ["taxiroute"],
                "polling_type": "route_distance_depended",
                "part_type": "taxiroute",
                "priority": 1
            },
            {
                "service": "eats",
                "part_name": "full_info",
                "url": "/some/eats/url",
                "fields": ["field1", "field2", "field3"],
                "polling_type": "tag_defined",
                "part_type": "eats_full",
                "priority": 4,
                "required": true
            }
        ]
    }
}
```

`known_orders` - optional

## Клиентская логика

- новый поллинг включается, когда в `launch` приходит объект `mlutp_orders_state` (раньше было условие по эксперименту, но данный вариант более гибок)
- добавляем объект `tags` в объект `mlutp_orders_state`, показывающий состояние актуальности отправленных данных. 
При получении, клиенты должны вызвать `mlutp/v1/orders/state` с объектом `tags`, который в свою очередь повторит попытку получения активных заказов(например).
Клиенты должны ожидать что количество заказов после вызова ручки `mlutp/v1/orders/state` может измениться.
- По причине возможного большого количества партов и полей в них, возможна проблема с их валидностью, из-за чего будет невозможно собрать карточку полностью. Для этого предлагается слать метрики в апметрику.

## Проблемы и их решения

`launch`:
- x2 запросов в сервис `order-state` из `launch`
- ручка `order-state/v1/orders/state` таймаутит или отдаёт 500
  - перестаём отдавать объект `mlutp_orders_state` (на этапе раскатки, далее собираем фолбек)
- ручка `order-core/active-orders` или `order-state/mlutp/v1/eats/orders/state` таймаутит или отдаёт 500
  - отдаём объект `tags` клиентам, для контроля актуальности данных на стороне клиента
  - для заказов такси, можно попробовать сформировать ответ из `feedbacks` | `protocol/launch`
- фолбек `polling-policy` и всего ответа `mlutp_orders_state`, понадобиться, после раскатки на 100% и стабилизации работы `launch` в таком режиме
