# Анализ метрики EventLoopLag в серверном эксперименте

Для корректной оценки влияния серверного эксперимента на ноду, нужно выбрать два четыре хоста (контроль/эксперимент и медленный/быстрый).
Провести эксперимет, а потом этим запросом сравнить значения метрик.

В данном примере анализируется метрика EventLoopLag. Для анализа используется 99 перцентиль. 

Теги: `event loop lag`, `серверные эксперименты`, `метрики скорости`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbXzwVK8P1EbnxxuduNIJJOkR_23Bc1pRgXMwjqJn4=

```sql
use marketclickhouse;

/*
Быстрый хост:
    - эксп: sas2-0243-52e-sas-market-prod--d06-23430.gencfg-c.yandex.net
- контроль: sas2-4939-fab-sas-market-prod--d06-23430.gencfg-c.yandex.net
Медленный хост:
    - эксп: sas6-1827-b04-sas-market-prod--d06-23430.gencfg-c.yandex.net
- контроль: sas6-1828-3a9-sas-market-prod--d06-23430.gencfg-c.yandex.net
*/

select
    host,
    round(quantile(0.99)(duration_ms)) as eventLoopLag99
from (
    select
    *
    from `market`.`market_frontend_timers`
    where
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and label = 'eventLoop'
        and type = 'maxLag'
        and environment = 'PRODUCTION'
        and service = 'market_front_desktop'
        and host in (
            'sas2-0243-52e-sas-market-prod--d06-23430.gencfg-c.yandex.net',
            'sas2-4939-fab-sas-market-prod--d06-23430.gencfg-c.yandex.net',
            'sas6-1827-b04-sas-market-prod--d06-23430.gencfg-c.yandex.net',
            'sas6-1828-3a9-sas-market-prod--d06-23430.gencfg-c.yandex.net'
        )
)
group by host;
```
