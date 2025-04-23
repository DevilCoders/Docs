## Поиск уже заказанных блюд

Задача:


Для [задачи сортировки блюд внутри категорий](https://st.yandex-team.ru/EDADEV-38051) необходимо научиться получать блюда, которые пользователь уже заказывал.

Решение:

В сервисе `eats-ordershistory` есть ручка `/v1/get-orders`, которая по `eater_id/user_id/yandex_uid` может отдать все заказы за последние 60 дней.
98 процентиль этой ручки держится в районе 50ms, за исключением выбросов.

Нас интересуют блюда, которые пользователь заказывал, их мы получим по каждому заказу в следующем виде:
```
        CartItem:
            type: object
            additionalProperties: false
            description: товарная позиция в корзине пользователя
            properties:
                place_menu_item_id:
                    description: идентификатор товара в меню ресторана
                    type: integer
                    format: int32
                product_id:
                    description: идентификатор товара
                    type: string
                name:
                    description: название товара, напрмер «картошка»
                    type: string
                quantity:
                    description: количество товаров в рамках этой позиции
                    type: integer
                    format: int32
            required:
              - place_menu_item_id
              - name
              - quantity
```

Поле `place_menu_item_id` соотвествует `id` в `ItemResponse` сервиса `eats-restaurant-menu`.

К сожалению, в ручке `/v1/get-orders` возвращается place_id для каждого заказа, а в сервисе `eats-restaurant-menu` мы не знаем его, поэтому приходится производить операции над всеми `place_menu_item_id`, которые нам вернула ручка.
А именно: создадим map<`place_menu_item_id`, `quantity`> по всем заказам, которые получили.

Таким образом, при необходимости отсортировать какую-либо категорию так, чтобы вначале шли блюда, которые пользователь заказывал большее количество, для каждого блюда можно будет получить это количество из map<`place_menu_item_id`, `quantity`>, а потом отсортировать по этому числу.
