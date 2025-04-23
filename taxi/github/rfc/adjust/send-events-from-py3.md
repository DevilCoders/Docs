# Задача

Нужно перенести отправку Adjust событий из backend в backend-py3. \
Тикет: [TAXIBACKEND-26599](https://st.yandex-team.ru/TAXIBACKEND-26599)

# Реализация
## uservices

На событие `handle_complete` процессинга 2.0 будем ставить stq-обработчики для отправки разных типов событий (успешный заказ, первого успешный заказ и в дальнейшем другие). Они, в свою очередь, будут ставить таску `add_adjust_event` на отправку события в Adjust.

Аргументы - `user_id`, `application`, `tariff`, `created_at` и прочую дополнительню информацию, записывающуюся в событие.

Ключ идемпотентности (`task_id`) для тасок, ставящихся из процессинга - order_id + тип события. \
Ключ идемпотентности (`task_id`) для `add_adjust_event` - сгенерированный uuid64. Будем генерировать его в самом конце. Это обеспечит уникальность ключа для каждого события.

Обновление [конфига](https://github.yandex-team.ru/taxi/uservices/blob/develop/services/processing/configs/config.user.yaml):
```yaml
  - name: add-success-tariff-adjust-event
    events:
      - key: handle_complete
    handler-config:
        enabled#and:
          - value#not:
                value#empty:
                    value#xget:
                        path: /order-proc/order/statistics/application
                        default-value: ''
          - value#not:
                value#empty:
                    value#xget:
                        path: /order-proc/order/performer/tariff/class
                        default-value: ''
    stq:
        queue: add_success_tariff_adjust_event
        task_id#xget: /order-proc/_id
        args#array: []
        kwargs:
            user_uid#xget: /order-proc/order/user_id
            application#xget: /order-proc/order/statistics/application
            tariff#xget: /order-proc/order/performer/tariff/class
            city#xget: /order-proc/order/city
            cost#xget: /order-proc/order/cost
            currency#xget: /order-proc/order/performer/tariff/currency
            created_at#timestamp-now: null

  - name: add-first-success-tariff-adjust-event
    events:
      - key: handle_complete
    handler-config:
        enabled#and:
          - value#not:
                value#empty:
                    value#xget:
                        path: /order-proc/order/statistics/application
                        default-value: ''
          - value#not:
                value#empty:
                    value#xget:
                        path: /order-proc/order/performer/tariff/class
                        default-value: ''
    stq:
        queue: add_first_success_tariff_adjust_event
        task_id#concat-strings:
          - value: /order-proc/order/user_phone_id
          - value: /order-proc/order/performer/tariff/class
        args#array: []
        kwargs:
            user_uid#xget: /order-proc/order/user_id
            phone_id#xget: /order-proc/order/user_phone_id
            application#xget: /order-proc/order/statistics/application
            tariff#xget: /order-proc/order/performer/tariff/class
            city#xget: /order-proc/order/city
            cost#xget: /order-proc/order/cost
            currency#xget: /order-proc/order/performer/tariff/currency
            created_at#timestamp-now: null
```

## backend-py3

### stq-worker `add_success_tariff_adjust_event`.

1. Проверяем, что application находится в конфиге `ADJUST_APPLICATIONS`.
1. Проверяем, что нужно отправлять события по данному тарифу в конфиге `ADJUST_CONFIG`.
1. Генерим ключ и ставим таску на отправку события


### stq-worker `add_adjust_first_order_event`

1. Проверяем, что application находится в конфиге `ADJUST_APPLICATIONS`.
1. Проверяем, что нужно отправлять события по данному тарифу в конфиге `ADJUST_CONFIG`.
1. Идем за статистикой в userstats по `phone_id` и `brand=APPLICATION_MAP_BRAND[application]` (количество заказов по разным тарифам).
1. В случае первого заказа по данному тарифу генерим ключ и ставим таску на отправку соответствующего события.

### stq-worker `add_adjust_event`

1. Ищем `user_id` в db.adjust_users (если не нашли, валимся).
2. Отправляем событие в Adjust.

## Отличия от существующей логики

1. За статистикой ходим в userstats, a не в db.user_phones
1. Не пишем таски в базу adjust_tasks в случае ошибки при отправке, а полагаемся на ретраи stq.

## Оценка по времени

[2d] Написание stq-workers \
[5h] Тестирование в тестинге \
[5h] Выпиливание старой логики + проверка, что события отправляются в одном экземпляре \
[6h] Ревью (все итерации)

**Итого: 4d**

