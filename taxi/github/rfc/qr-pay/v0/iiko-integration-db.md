# Что
Делаем базу для хранения ресторанных (пред)заказов, приходящих со стороны ресторанной системы iiko.

# Почему
Потому-что заказ в Еде обязательно нужно создавать уже с пользователем, а Еда не успеет сделать такой же функционал (сервис для хранения драфтов заказов) к deadline-у.

# Хранимые данные
Сохраняем каждый приходящий от ресторанов заказ в таблице со следующей структурой:

```sql
CREATE SCHEMA iiko_integration;

CREATE TYPE ORDER_ITEM AS (
    product_id text,
    parent_product_id text,
    name text,
    quantity numeric,
    price_per_unit numeric,
    price_without_discount numeric,
    price_for_customer numeric,
    discount_amount numeric,
    discount_percent numeric,
    vat_amount numeric,
    vat_percent numeric
);

CREATE TABLE IF NOT EXISTS iiko_integration.orders (
    id text PRIMARY KEY,
    idempotency_token text NOT NULL,
    restaurant_id text NOT NULL,
    expected_cashback_percentage numeric NOT NULL,
    status text NOT NULL,
    total_price numeric NOT NULL,
    discount numeric,
    currency text NOT NULL,
    items ORDER_ITEM[] NOT NULL,
    created_at timestamptz NOT NULL DEFAULT NOW(),
    updated_at timestamptz NOT NULL DEFAULT NOW()
);
```

CREATE UNIQUE INDEX IF NOT EXISTS idempotency_idx ON iiko_integration.orders (idempotency_token, restaurant_id);

CREATE INDEX IF NOT EXISTS orders_restaurant_id_idx ON iiko_integration.orders (restaurant_id);

CREATE INDEX IF NOT EXISTS orders_created_at_idx ON iiko_integration.orders (created_at);


### Про discount
Ресторан со своей стороны может предоставлять любые скидки - нас это не касается, мы считаем кешбек и всё остальное от итоговой цены которую ресторан берёт с клиента

Ресторан будет передавать скидку (процент и сумму) для каждого элемента заказа, а также общую скидку (сумму)

### Почему делаем схему для OrderItem а не храним JSON
Это оказалось проще чем городить трансформацию типов в логике работы с базой - можем использовать нативные типы для decimal-значений.
Также бонусом это более правильно (не произвольный json а нормальный тип) и занимает меньше места в базе.

### Про expected_cashback_percentage
При создании нового заказа мы записываем актуальное на тот момент значение кешбека для заказа в сам заказ.
При начислении кешбека бы берём из базы total_price и expected_cashback_percentage и считаем из них кешбек.

# Сколько храним данные
Пока мы используем бэкенд Еды для работы с заказами, а именно - для получения истории заказов, - нет смысла хранить в этой базе заказы долгое время. Предлагается удалять из базы заказы старше какого-то времени - задать в конфиге timeout для протухания заказа, и удалять крон-таской все заказы, у которых created_at (updated_at?) старше.

# Изменения в запланированом flow
Следует вынести всю логику завязанную на том что `restaurant_id` является частью `order_id`. Вместо этого необходимо идти в базу по order_id и доставать restaurant_id оттуда.

Возможно следует перенести расчёт значения кешбека в ручку iiko, создающую заказ.