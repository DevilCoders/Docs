# Детализация фаз http(s) запросов + время на парсинг и Buffer.toString (parse)

Агрегация метрик длительности фаз http(s) запросов bcm2-ручки с интервалом в 30 минут. Удобно для построения графиков.

Теги: `http phases`, `метрики скорости`.

Ссылка: https://yql.yandex-team.ru/Operations/YUHlA9jKS5vGIWPaoEwplmAONhiXHTnlOhwuY6vTmsU=

```sql
use marketclickhouse;

select
    toStartOfInterval(toDateTime(timestamp), INTERVAL 30 minute) as t,
    kv_keys as metrics,
    quantileTiming(0.99)(toInt32OrZero(kv_values)) as values
from market.market_front_trace
array join kv_keys, kv_values
where
    date = today()
    and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now()) 
    and source_module = 'market_front_desktop'
    and environment = 'PRODUCTION'
    and request_method = 'fetchPrime'
    and metrics in 
        ('httpTcp', 'httpTls', 'httpDownload', 'httpRequest', 'httpDns', 'httpFirstByte', 'httpWait', 'httpTotal', 'parse')
group by metrics, t
order by t;
```
