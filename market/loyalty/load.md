# Про стрельбы

Для стрельбы поднимаем свой меленький балансер на хосте market-loyalty-admin (не market-loyalty, чтобы меньше влиять на картину). 
Для этого идем в интснас няни и [запускаем](market-loyalty-admin/src/main/external/load/start_balancer.sh)
Поднимется nginx на порту 14330, который будет проксировать запросы на market-loyalty, по нему и стреляем

Сборную информацию (sla + факт) храним [здесь](https://wiki.yandex-team.ru/users/gnefedev/loyalty/sla/), патроны - complex_load.py 

После каждой стрельбы обновляем цифры и пишем в комент как минимум стрельбу, а также что было изменено в сервисе и изменения фактических показателей.
Результаты фиксируем по стрельбе, которую оставляли на ночь (часов 8-10)

99 и 99.9 персентили берем из графаны в период стрельб: максимальные пики соответсвующих поручечных графиков.

Кроме обычной стрельбы периодически нужно проводить стрельбы с 10-кратным rps и убеждаться, что приложение восстанавливается само.
profile: line(1x, 10x, 30m) line(10x, 1x, 30m)

В случае кеширования в ручке, при расчете уникальных пользователей необходимо учитывать глубину и длительность сессии, 
чтобы получить правильный cache hit

Для подсчета персентилей по КХ есть запрос:
```sql
SELECT page_id, max(duration_999), max(duration_99), max(duration_95)
FROM (SELECT page_id, quantileTiming(0.999)(duration_ms) as duration_999, quantileTiming(0.99)(duration_ms) as duration_99, quantileTiming(0.95)(duration_ms) as duration_95
      FROM market_loyalty
      WHERE "date" = today()
        AND environment = 'TESTING'
        AND type = 'IN'
        AND page_id <> 'ping_using_get'
        AND page_id <> 'get_stat_using_get'
        AND page_id <> 'spend_discount_using_post'
        AND page_id <> 'get_documentation_using_get'
        AND page_id <> 'order_status_updated_using_post'
        AND page_id <> 'get_coupon_using_get'
        AND page_id <> 'activate_coupons_using_post'
        AND page_id <> 'revert_discount_using_post'
        AND page_id <> 'create_coin_using_post'
        AND "timestamp" >= toUInt32(toDateTime('2018-10-22 15:00:00'))
        AND "timestamp" <= toUInt32(toDateTime('2018-10-22 17:30:00'))
    GROUP BY toStartOfFiveMinute(toDateTime("timestamp")), page_id
) GROUP BY page_id;
```
