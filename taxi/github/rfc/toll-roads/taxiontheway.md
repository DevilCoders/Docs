## Проработка TOTW (api-proxy) для Платных дорог

### Назначение
Передавать клиентам 2 параметра:
- как отрисовывать маршрут (по платной или бесплатной дороге)
- возможность пользователя сменить тип маршрута на бесплатный/платный

### Реализация
При запросе `/3.0/taxiontheway` (через _api-proxy_) делаем запроc в сервис `toll-roads`

```
POST /toll-roads/v1/order/retrieve {"order_id": "58a889e1404a2b8fa892cd7edcf26667"}
{"has_toll_roads": true, "can_switch_road": true, "auto_payment": false}
```

Для клиентов выглядит так:

```
POST /3.0/taxiontheway {...}
{
    ....
    "toll_roads": {
        "has_toll_roads": true,
        "can_switch_road": true,
        "auto_payment": false,
    },
    ...
}

Изменение схемы:
    ...
    toll_roads:
        type: object
        properties:
            has_toll_road:
                type: boolean
                description: Содержит ли выбранный маршрут платный участок
            can_switch_road:
                type: boolean
                description: Возможна ли смена типа маршрута
            auto_payment:
                type: boolean
                description: Будет ли автоматическое списание средств за платную дорогу
    ...
```

Условия для _api-proxy_:
- поход в сервис под экспериментом `totw_use_toll-roads` для того, чтобы иметь возможность постепенно наращивать нагрузку на сервис `toll-roads`
- поход в сервис, если определено значение `order_proc.order.request.toll_roads`
