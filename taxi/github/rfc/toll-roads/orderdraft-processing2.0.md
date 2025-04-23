# OrderDraft + Processing2.0

Необходимо:
1. принять объект `toll_roads` с двумя полями `user_had_choice` и `user_chose_toll_road` от клиента в запросе orderdraft. сам объект `toll_roads` optional, а его поля required.
1. сохранить `toll_roads` в объекте `order_proc.order.request`
1. с помощью [processing 2.0](https://wiki.yandex-team.ru/taxi/backend/architecture/processing/manual/) запустить STQ-таску [toll_roads_order_save](service.md#toll_roads_order_save)

## Расширение запроса orderdraft

Добавляем optional структуру `toll_roads` в [orderdraft.yaml](https://github.yandex-team.ru/taxi/backend-cpp/blob/develop/protocol/docs/protocol/yaml/orderdraft.yaml)

```yaml
definitions:
    OrderdraftRequest:
        properties:
        ...
            toll_roads:
                description: информация о выборе платной дороги
                $ref: definitions.yaml#/definitions/toll_roads
```
и в [definitions.yaml](https://github.yandex-team.ru/taxi/backend-cpp/blob/develop/protocol/docs/protocol/yaml/definitions.yaml)
```yaml
definitions:
    toll_roads:
        additionalProperties: false
        description: информация о выборе платной дороги
        properties:
            user_had_choice:
                description: был ли у пассажира выбор между бесплатной и платной дорогами
                type: boolean
            user_chose_toll_road:
                description: |
                    какой выбор был сделан пассажиром (либо какой был единственно возможный выбор)
                    между бесплатной(false) и платной(true) дорогой.
                type: boolean
        required:
            - user_had_choice
            - user_chose_toll_road
        type: object
```

## Изменения логики ручки orderdraft

В ручке orderdraft сохраняем `toll_roads` из `OrderdraftRequest` в объекте `order_proc.order.request`.

## Конфигурация processing2.0 для STQ-таски toll_roads_order_save

Добавляем в секцию `yaml-handlers` [конфигурации](https://github.yandex-team.ru/taxi/uservices/blob/develop/services/processing/configs/config.user.yaml) сервиса processing следующее:

```yaml
- name: toll_roads_order_save
  events:
    - reason: create
  handler-config:
    enabled: true
    stq:
      queue: toll_roads_order_save
      task_id#xget: /order-proc/_id
      args#array: []
      kwargs:
        created#xget: /order-proc/created
        order_id#xget: /order-proc/_id
        offer_id#xget:
          path: /order-proc/order/request/offer
          default-value: ''
        user_had_choice#xget:
          path: /order-proc/order/request/toll_roads/user_had_choice
          default-value: false
        user_chose_toll_road#xget:
          path: /order-proc/order/request/toll_roads/user_chose_toll_road
          default-value: false
```
Это означает, что будет запущена STQ-таска [toll_roads_order_save](service.md#toll_roads_order_save) на этапе create.

Использование `order_id` в качестве `task_id` позволяет избежать накопления нескольких одинаковых тасков в очереди STQ, что служит целям оптимизации. Идемпотентность же таски обеспечивается её обработчиком, что описано в [toll_roads_order_save](service.md#toll_roads_order_save). 
