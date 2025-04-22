# Проактивный саппорт. Исключение дублей.

## Текущее решение:

Каждые 5 минут мы берем все заказы, которые были созданы позже now() - config.EATS_PROACTIVE_SUPPORT_SELECT_INTERVAL_SEC. Таким образом, если config.EATS_PROACTIVE_SUPPORT_SELECT_INTERVAL_SEC больше, чем 5 минут, то заказы могут дублироваться.

## Задача:

Избежать дублирования заказов в сообщениях от бота.

## Решение:

### Основная идея:
В сервисе eda-region-points заведем Postgres. 

И табличку:
```
CREATE TABLE IF NOT EXISTS proactive_support.notified_orders
(
    order_nr TEXT PRIMARY KEY,
    notified_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

В этой табличке мы будем хранить все заказы, по которым мы отправили уведомление за прошлые EATS_PROACTIVE_SUPPORT_SAVE_NOTIFIED_ORDERS_INTERVAL_SEC секунд, где EATS_PROACTIVE_SUPPORT_SAVE_NOTIFIED_ORDERS_INTERVAL_SEC - конфиг.

Самым оптимальным значением EATS_PROACTIVE_SUPPORT_SAVE_NOTIFIED_ORDERS_INTERVAL_SEC - является config.EATS_PROACTIVE_SUPPORT_SELECT_INTERVAL_SEC + eps, где eps - время выполнения крон таски. 

### Механика отсечения дублей:

После получения всех заказов за последние config.EATS_PROACTIVE_SUPPORT_SELECT_INTERVAL_SEC секунд мы будем брать все заказы, которые лежат в нашей таблицы, и отправлять сообщения только с теми заказами, которых не было в ней.

В конце каждой крон таски мы будем добавлять в таблицу заказы, которые были только что отправлены в телеграмм бот, а также удалять те заказы, о которых мы оповещали больше, чем EATS_PROACTIVE_SUPPORT_SAVE_NOTIFIED_ORDERS_INTERVAL_SEC секунд назад


## Преспектива перехода на updated_at:

Есть идея брать заказы которые были НЕ созданы, а обновлены позже now() - config.EATS_PROACTIVE_SUPPORT_SELECT_INTERVAL_SEC. Для этого перехода нам понадобится помимо времени хранить "статус заказа" на который обновился выбранный заказ.
