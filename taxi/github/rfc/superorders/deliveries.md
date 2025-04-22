# Проработка доставок:

## Доставка из ПВЗ

[Проработка флоу заказа посылки](https://github.yandex-team.ru/taxi/rfc/pull/375/files)

### launch

Точки входа заказа посылок - не меняются(пуш, либо пришедший список посылок в поле `shipments` лонча, сам заказ делается через саммари).
Заказы сделаные через флоу достаки - прорастают как обычные заказы такси.

### Реализация в новой системе полинга
- Для нового флоу, необходимо, после создания заказа, передавать его в [`4.0/mlutp/orders/state`](https://github.yandex-team.ru/taxi/rfc/blob/master/superorders/stage_1.md)
- Полить ручки отвечающие за полученые парты в соответсвии `policy` получеными в `launch`. На этапе 1, будет использоваться ручка [taxi/v1/orders/state](https://github.yandex-team.ru/taxi/rfc/blob/master/protocol/mlutp_v1_taxi_v1_orders_state.md)

## Пророщенный заказ

[Проработка пророщеного заказа](https://github.yandex-team.ru/taxi/rfc/pull/332/files)

### launch

Клиент получает заказы из launch в поле 

```(json)
"shared_orders": [
	{
		"key": "1",
		"status": "waiting"
	}
]
```

### polling

Если если заказ в нетерминальном статусе, то начинает полится ручка `shareroute/info`
Полится ручка `sharedroute/track` если в ответе `shareroute/info` поле `show_track: true`
Могут полится параллельно. track - имеет в своём составе часто меняющиеся данные, info - редко

Значение поля `show_track` - зависит от статуса заказа.

### Реализация в новой системе полинга

Вводим новый тип сервиса: `shared_route` с партами `track` и `info`

1. Добавляем поход в `/v1/sharing_keys` для получения списка заказов из `v1/orders/state`.
2. Для парта track нужно использовать логику выставления флага `show_track` для добавление этого парта в `need_requests`
3. Необходимо реализовать батчовые ручки трекинга и получения информации (возможно, можно жить и на текущих ручках  какое-то время, но тогда нужно не забыть при переезде поменять название партов).

Пример запроса в `4.0/mlutp/orders/state`

```(json)
{
    "known_orders": [
        {
            "orderid": "order1",
            "status": "transpoting",
            "tags": {
                "track": "1590674415",
                "info": "1590674415",
            },
            "force": true,
            "service": "shared_route"
        }
    ]
}
```

Ответ
```(json)
{
    "orders": [
        {
            "orderid": "order1",
            "service": "shared_route",
            "status": "transpoting", # в этапе 1 данный статус возвращается тот же, что нам прислали клиенты
            "need_request": ["track", "info"],
            "tags": {
                "track": "1590674416",
                "info": "1590674416",
            },
            "update_status": "actual"
        }
    ],
    "allowed_changes": [
        {
            "service": "shared_route",
            "can_make_more_orders": false # ?? вроде бы сам клиент заказ сделать не может
        },
    ]
}
```

Пример АПИ батчовых ручек

```(json)
{
    "force": true | false,
    "orders": [
        {
            "orderid":"777777-888888",
            "track": "encoded_part_tag"
        }
    ]
}
```

```(json)
{
    "orders": [
        {<any fields for orderid 777777-888888>}
    ]
}
```
