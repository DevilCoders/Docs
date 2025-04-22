# Библиотека полезных запросов

> Содержимое генерируется автоматически! Для обновления нужно воспользоваться репозиторием в монорепе (https://github.yandex-team.ru/market/monomarket/tree/master/lib/scripts/queries). Любые изменения на Вики будут перезаписаны!

### Примеры запросов Здоровья
- https://wiki.yandex-team.ru/market/verstka/health/#primeryzaprosov
- https://wiki.yandex-team.ru/Market/frontend/Partner/health/#bazaclickhouse

---

Всего собрано запросов: 22.

Доступные теги: `клиентские эксперименты`, `ttr`, `tti`, `dcl`, `loaded`, `test id`, `метрики скорости`, `ttlb`, `агрегированная метрика`, `виджеты`, `первый экран`, `errors`, `http phases`, `бакеты`, `сплиттинг`, `kpi`, `report`, `resource`, `серверные эксперименты`, `event loop lag`, `кракен`, `виджет`, `рендеринг`, `тестирование`, `км`, `ошибки`, `трассировка`, `анализ деградации`, `resolver`, `резолвер`.

---

# Расчет клиентских экспериментов

Сравнение клиентских метрик по сплита эксперимента на выбранных страницах.

Теги: `клиентские эксперименты`, `ttr`, `tti`, `dcl`, `loaded`.

Ссылка: https://yql.yandex-team.ru/Operations/XwLdz5dg8mTi5L8ExiA50ycSSO0eqVTPKdMim12ugTw=

```sql
use marketclickhouse;

select 
    a.split as split,
    page_id,
    
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms, portion = 'firstScreen') as TTR,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'firstScreen') as TTI,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'domContentLoaded') as DCL,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'loaded') as loaded,
    
    uniq(a.request_id) as hits

from (
    select 
        x_market_req_id
    from market.slb_balancer
    where
        date between toDate(now() - interval '2' DAY) and toDate(now())
        and host = 'beru.ru'
        and method = 'GET'
        and is_robot = 'false'
) as b

inner join (
    select 
        request_id,
        page_id, 
        portion, 
        timestamp_ms, 
        start_time_ms, 
        duration_ms,
        arrayJoin(['off','lazy']) as split
        
    from market.market_client_timers 
    
    where 
        date between toDate(now() - interval '2' DAY) and toDate(now())
    
        and platform = 'web'
        and vhost = 'beru.ru'
        and name = 'page'
        and page_id in(
            'blue-market:index',
            'blue-market:product', 
            'blue-market:list', 
            'blue-market:cart', 
            'blue-market:search',
            'blue-market:catalog'
        )
        and portion in('firstScreen', 'domContentLoaded', 'loaded')
        and position(info_values[indexOf(info_keys, 'expFlags')], concat('all_speed_lazy-loaded-pics', '=', split)) != 0
) as a

on b.x_market_req_id = a.request_id

group by a.split, page_id
order by page_id;
```

---

# Расчет клиентских метрик клиентских экспериментов по testid-ам

Анализ клиентского эксперимента. Анализируются клиентские метрики. Данные группируются по сплитам (test-id) и страницам. 

Теги: `клиентские эксперименты`, `test id`, `ttr`, `tti`, `dcl`, `loaded`, `метрики скорости`.

Ссылка: https://yql.yandex-team.ru/Operations/YLTvpfMBw877XKd6Dg3XHcU1cj2HDKj3TPG-z8LUDjk=

```sql
use marketclickhouse;

select 
    a.split as split,
    page_id,
    
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms, portion = 'firstScreen') as TTR,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'firstScreen') as TTI,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'domContentLoaded') as DCL,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'loaded') as loaded,
    
    uniq(a.request_id) as hits

from (
    select 
        x_market_req_id
    from market.slb_balancer
    where
        date between toDate(now() - interval '2' DAY) and toDate(now())
        and host = 'market.yandex.ru'
        and method = 'GET'
        and is_robot = 'false'
) as b

inner join (
    select 
        request_id,
        page_id, 
        portion, 
        timestamp_ms, 
        start_time_ms, 
        duration_ms,
        arrayJoin(['353706','353709', '353713']) as split
        
    from market.market_client_timers 
    
    where
        date between toDate(now() - interval '2' DAY) and toDate(now())
    
        and platform = 'web'
        and vhost = 'market.yandex.ru'
        and name = 'page'
        and page_id in(
            'market:index',
            'market:product', 
            'market:list', 
            'market:search',
            'market:catalog'
        )
        and portion in('firstScreen', 'domContentLoaded', 'loaded')
        and position(info_values[indexOf(info_keys, 'testIds')], split) != 0
) as a

on b.x_market_req_id = a.request_id

group by a.split, page_id
order by page_id, a.split
```

---

# Расчет TTLB клиентских экспериментов по testid-ам

Анализ клиентского эксперимента. Анализируется TTLB. Данные группируются по сплитам (test-id) и страницам.

Теги: `клиентские эксперименты`, `test id`, `ttlb`, `метрики скорости`.

Ссылка: https://yql.yandex-team.ru/Operations/YLT4ehJKfYEUqJnx-fxiAt_3lZozrTJAuohMoOYdIGk=

```sql
use marketclickhouse;

select 
    a.split as split,
    page_id,

    quantileTiming(0.95)(resptime_ms) as TTLB,
    
    uniq(a.req_id) as hits

from (
    select
        host, 
        req_id, 
        resptime_ms,
        page_id,
        arrayJoin([353706, 353709, 353713]) as split
    from market.nginx2
    where
        date between toDate(now() - interval '2' DAY) and toDate(now())
        and vhost = 'market.yandex.ru'
        and has(`test_id`, split)
        and page_id in(
            'market:index',
            'market:product', 
            'market:list', 
            'market:search',
            'market:catalog'
        )
) as a

group by a.split, page_id
order by page_id, a.split;
```

---

# Клиентские метрики по виджетам на KPI-страницах

Было проведено исследование о том, как мы считаем наши TTR и TTI (https://st.yandex-team.ru/MARKETFRONTECH-2531).

Исходя из исследования, если взять top-1 строчку по каждой странице, это будет TTR/TTI страницы.

Наша агрегированная метрика: https://datalens.yandex-team.ru/4gcgvlxhzqnaz-need-for-speed-po-celevym-stranicam.

Табличка кликфита с данными: https://health.market.yandex-team.ru/projects/marketfrontend/clickphite/configs/front_speed_kpi_region_filtered/4/edit/json

Код в мандреле: https://github.yandex-team.ru/market/monomarket/blob/master/lib/lib/mandrel/src/launchClient/timers.js#L123.

Эта таблица -- попытка детализировать данные агрегированной метрики.

Теги: `агрегированная метрика`, `виджеты`, `ttr`, `tti`, `метрики скорости`, `первый экран`.

Ссылка: https://yql.yandex-team.ru/Operations/YLD34PMBw877WwUPyvsz_FfZdhw8RJhnXIAHflim4W8=

```sql
use marketclickhouse;

/* TTR и TTI в белом */
select
    service,
    page_id,
    widgetName,
    round(quantile(0.95)(TTI)) as TTI_p95,
    round(quantile(0.95)(TTR)) as TTR_p95,
    round(quantile(0.95)(hydrating)) as hydrating_p95,
    round(quantile(0.95)(stuffing)) as stuffing_p95,
    count(*) as hits
  from (
    select
        *,
        info_values[indexOf(info_keys, 'widgetName')] as widgetName,
        info_values[indexOf(info_keys, 'onFirstScreen')] as onFirstScreen,
        /*
            Страничный TTI считается по формуле
            timestamp_ms - start_time_ms + duration_ms (0.95)
            здесь timestamp -- firstScreen.arrived
                duration -- firstScreen.inited - firstScreen.arrived

            то есть страничный TTI = firstScreen.inited - start_time_ms
            firstScreen.inited = max(ProcessedWidgetReport.timings.inited)

            timings.inited не пишется, зато пишутся timings.arrived, timings.hydrated, timings.duration.stuffing, timings.duration.hydrating

            timings.inited = widgetType === 'static' ? timings.arrived : timings.hydrated;

            Пренебрежение: все виджеты с высокими таймингами не статические
            для грубой оценки можно использовать round(quantile(0.95)(duration_ms))
        */
        timestamp_ms + duration_ms as hydrated,
        hydrated - start_time_ms as TTI,

        /*
            Страничный TTR считается по формуле
            timestamp_ms - start_time_ms (0.95)
            здесь timestamp -- firstScreen.arrived
        */
        timestamp_ms - start_time_ms as TTR,

        /*
            Для полноты картины взглянем на новые метрики
        */
        toInt64(info_values[indexOf(info_keys, 'hydrating')]) as hydrating,
        toInt64(info_values[indexOf(info_keys, 'stuffing')]) as stuffing
      from `market`.`market_client_timers`
     where date = toDate('2021-05-17')
       and page_id in ('market:index', 'market:search', 'market:list', 'market:product', 'touch:index', 'touch:search', 'touch:list', 'touch:product')
       and service in ('market_front_desktop', 'market_front_touch')
       and name = 'widget'
  )
 where onFirstScreen = 'true'
 group by service, page_id, widgetName
 having hits > 7000
 order by page_id asc, TTI_p95 desc, TTR_p95 desc;
```

---

# JOIN запросов в nginx и ошибок приложения по requestId

Агрегирует данные из таблицы ошибок с таблицей nginx2.

Теги: `errors`.

Ссылка: https://yql.yandex-team.ru/Operations/XuIEjWim9YmO-YY6fV6G8XgulL86A2Qi0rhyItNDmD4=

```sql
use marketclickhouse;

select 
    *
from (
    select
        *
    from market.nginx2
    where 
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'   
) nginx

right join

(
    select
        request_id
    from market.market_errors
    where
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'
        and message like '%CartList%'
        and code = 'FailedViewError'
        and service like '%market_front_%'
) front_errors

on nginx.req_id = front_errors.request_id;
```

---

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

---

# Метрика с разбивкой на бакеты

Строит последовательность метрики TTI с интервалом в 10 минут, разбитую на бакеты.

Квантили не всегда удобны для анализа, особенно когда изменяется rps. Если требуется исследовать ухудшились/улучшились временные метрики или добавилось/убавилось быстрых/медленных запросов стоит проверить графики с разбивкой по бакетам - подсчёт количества запросов для которых метрика укладывается в некий интервал. Бакеты можно выбирать произвольные, но обычно удобнее всего использовать логарифмическую шкалу.

Теги: `бакеты`, `сплиттинг`, `tti`.

Ссылка: https://yql.yandex-team.ru/Operations/YVarg5fFtzcrh6axcG4GLmoiBIfiNkMG0JAbLsn2fKg=

```sql
use marketclickhouse;

select 
    toStartOfTenMinutes(toDateTime(timestamp)) as time, 
    pow(2, ceil(log2(timestamp_ms - start_time_ms + duration_ms))) as bucket, 
    count() as cnt
from market.market_client_timers
where date = today()
    and vhost = 'market.yandex.ru'
    and portion = 'firstScreen'
    and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
    
group by time, bucket
order by bucket desc, time asc;
```

---

# Методы ресурса Репорта по частоте использования на KPI страницах

Запрос позволяет ответить на вопрос, какие ручки репорта мы используем чаще всего на KPI-страницах сервиса. Так же удобно посмотреть, какие именно ручки на каких страницах используются.

Теги: `kpi`, `report`, `resource`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbPEK5ODy4UJZZDXLhaeAvAs-YBhtFaWTCh-SOuq4g=

```sql
use marketclickhouse;

select 
    *
  from (
    select
         request_method,
         count() cnt,
         groupUniqArray(page_id)
      from market.trace
     where date = today()
       and type = 'OUT'
       and target_module = 'market_report'
       and environment = 'PRODUCTION'
       and source_module = 'market_front_desktop'
       and page_id in ('market:product', 'market:search', 'market:index', 'market:list')
       group by request_method
       order by cnt desc
  )
 where cnt > 1000;

select 
    *
  from (
    select
         request_method,
         count() cnt,
         groupUniqArray(page_id)
      from market.trace
     where date = today()
       and type = 'OUT'
       and target_module = 'market_report'
       and environment = 'PRODUCTION'
       and source_module = 'market_front_touch'
       and page_id in ('touch:search', 'touch:product', 'touch:list', 'touch:index')
       group by request_method
       order by cnt desc
  )
 where cnt > 1000;
```

---

# Плейсы Репорта по частоте использования на KPI страницах с привязкой к методам ресурса Репорта

Запрос позволяет ответить на вопрос, какие плейсы репорта мы используем чаще всего на KPI-страницах сервиса. Кроме того, запрос показывает связь `РУЧКА РЕПОРТА` - `МЕТОД РЕСУРСА РЕПОРТА`.

Теги: `kpi`, `report`, `resource`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbRxgVK8P1Ebnfje6FrZh2Xp9XR5JTtw35nBbdrFeg=

```sql
use marketclickhouse;

select
    page_id,
    extractURLParameter(query_params, 'place') as place,
    count() cnt,
    groupUniqArray(request_method) as requests_methods
  from market.trace
 where date = today()
   and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
   and type = 'OUT'
   and target_module = 'market_report'
   and environment = 'PRODUCTION'
   and source_module = 'market_front_desktop'
   and page_id in ('market:product', 'market:search', 'market:index', 'market:list')
 group by place, page_id
 order by page_id, cnt desc;

 select
    page_id,
    extractURLParameter(query_params, 'place') as place,
    count() cnt,
    groupUniqArray(request_method) as requests_methods
  from market.trace
 where date = today()
   and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
   and type = 'OUT'
   and target_module = 'market_report'
   and environment = 'PRODUCTION'
   and source_module = 'market_front_touch'
   and page_id in ('touch:search', 'touch:product', 'touch:list', 'touch:index')
 group by place, page_id
 order by page_id, cnt desc;
```

---

# TTLB, TTR и TTI по сервисам и страницам

Большая таблица с аггрегацией всех основных метрик по сервисам и страницам.
Позволяет удобно взглянуть на клиентские метрики страницы по хостам.

Теги: `агрегированная метрика`, `ttr`, `tti`, `ttlb`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbb45fFtzcrh8hpyGOZKKw-e8UXJGqzl8wX_tIP_pI=

```sql
use marketclickhouse;

select
    request_id,
    timestamp,
    host,
    service,
    page_id,
    request_TTLB,
    request_TTR,
    request_TTI
from (
    select
        timestamp,
        page_id,
        service,
        timestamp_ms - start_time_ms as request_TTR,
        timestamp_ms - start_time_ms + duration_ms as request_TTI,
        request_id
    from `market`.`market_client_timers`
    where
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and service in ('market_front_desktop', 'market_front_touch')
        and name = 'page'
        and portion = 'firstScreen'
        and request_id != ''
) as client_timers inner join (
    select
        host,
        req_id as request_id,
        resptime_ms as request_TTLB
    from market.nginx2
    where 
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'
        and service in ('desktop', 'touch')
        and req_id != ''
        and resptime_ms != 0
) as server_timers
on client_timers.request_id = server_timers.request_id;
```

---

# Расчет серверных экспериментов

Если при выкатке серверного эксперимента не была явно выделена контрольная группа, её можно составить вручную, но требуется чтобы в ней было такое же количество хостов как в группе эксперимента. Успешность разбивки на группы можно проверить по метрике hits - она должна быть равна в обоих группах.

Теги: `серверные эксперименты`, `ttlb`, `ttr`, `tti`, `dcl`, `loaded`, `метрики скорости`.

Ссылка: https://yql.yandex-team.ru/Operations/YVatlK5ODy4UJX4K_qLBsNKgPbC7m4R928-mjTL36rE=

```sql
use marketclickhouse;

select
    case
        when has(array(
            'iva1-1308-64b-iva-market-prod--85a-21130.gencfg-c.yandex.net', 
            'vla3-1729-386-vla-market-prod--2e3-14470.gencfg-c.yandex.net', 
            'sas2-0076-be0-sas-market-prod--291-20660.gencfg-c.yandex.net', 
            'iva1-1309-109-iva-market-prod--85a-21130.gencfg-c.yandex.net', 
            'iva1-1310-38b-iva-market-prod--85a-21130.gencfg-c.yandex.net', 
            'vla3-1734-44c-vla-market-prod--2e3-14470.gencfg-c.yandex.net', 
            'sas2-0140-f6b-sas-market-prod--291-20660.gencfg-c.yandex.net', 
            'iva1-1311-795-iva-market-prod--85a-21130.gencfg-c.yandex.net'
    ), host) then 'node8'
        when has(array(
            'iva1-1312-608-iva-market-prod--85a-21130.gencfg-c.yandex.net', 
            'vla3-1742-ce0-vla-market-prod--2e3-14470.gencfg-c.yandex.net', 
            'sas2-0214-985-sas-market-prod--291-20660.gencfg-c.yandex.net', 
            'iva1-1313-be3-iva-market-prod--85a-21130.gencfg-c.yandex.net', 
            'iva1-1315-c1b-iva-market-prod--85a-21130.gencfg-c.yandex.net', 
            'vla3-1751-0c9-vla-market-prod--2e3-14470.gencfg-c.yandex.net', 
            'sas2-0243-bf0-sas-market-prod--291-20660.gencfg-c.yandex.net', 
            'iva1-2158-04d-iva-market-prod--85a-21130.gencfg-c.yandex.net'
        ), host) then 'node12'
        else 'other'
    end as split,
    quantileTimingIf(0.95)(resptime_ms, portion = 'firstScreen') as TTLB,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms, portion = 'firstScreen') as TTR,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'firstScreen') as TTI,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'domContentLoaded') as DCL,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'loaded') as loaded,
    uniq(request_id) as hits

from (
    select
        timestamp, timestamp_ms, start_time_ms, duration_ms, portion, request_id
    from market.market_client_timers
    where date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and vhost = 'm.market.yandex.ru'
) as timers

left join (
    select
        host, req_id, resptime_ms
    from market.nginx2
    where date = today()
        and vhost = 'm.market.yandex.ru'
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
) as nginx
    on timers.request_id = nginx.req_id

group by split;

```

---

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

---

# Анализ динамики TTLB в ходе серверннго эксперимента на Кракене

Позволяет оценить влияние включения/отключения серверного эксперимента на Кракене. По таблице можно построить удобный график.

Теги: `ttlb`, `серверные эксперименты`, `метрики скорости`, `кракен`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbaPhJKfZcFg_z5HBfuGllS_GvuAEMU92EKdK-0Lsk=

```sql
use marketclickhouse;

select
    x,
    round(quantile(0.99)(resptime_ms)) as ttlb99
from (
    select
        *,
        toStartOfFiveMinute(toDateTime(timestamp)) as x
    from market.nginx2
    where
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'
        and host in (
            'vla3-1713-ab3-vla-market-prod-f-e0b-8041.gencfg-c.yandex.net'
        )
        and service = 'desktop'
        and page_id = 'market:search'
)
group by x
order by x;
```

---

# Анализ времени рендеринга выбранного виджета в серверном эксперименте

Для корректной оценки влияния серверного эксперимента на ноду, нужно выбрать два четыре хоста (контроль/эксперимент и медленный/быстрый).
Провести эксперимет, а потом этим запросом сравнить значения метрик.

В данном примере анализируется время рендеринга выбранного виджета. Для анализа используется 99 перцентиль.

Теги: `виджет`, `рендеринг`, `серверные эксперименты`, `метрики скорости`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbZkgVK8P1Ebn2o3VNdJ6KmGhXaKvr3J5c_JJnyvJg=

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

---

# Метрики скорости

Серверные и клиентские метрики скорости сервиса.

Теги: `метрики скорости`, `ttlb`, `ttr`, `tti`, `dcl`, `loaded`.

Ссылка: https://yql.yandex-team.ru/Operations/YVap5tK3DHqKY_UyNPWVr3bLB48HRGPevXhn7YuedXE=

```sql
use marketclickhouse;

select
    quantileTimingIf(0.95)(resptime_ms, portion = 'firstScreen') as TTLB,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms, portion = 'firstScreen') as TTR,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'firstScreen') as TTI,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'domContentLoaded') as DCL,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms + duration_ms, portion = 'loaded') as loaded

from (
    select
        timestamp,
        timestamp_ms,
        start_time_ms,
        duration_ms,
        portion,
        request_id
    from market.market_client_timers
    where date = today()
        and vhost = 'market.yandex.ru'
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())     
) as timers

left join (
    select
        host, req_id, resptime_ms
    from market.nginx2
    where date = today()
        and vhost = 'market.yandex.ru'
        aand timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
) as nginx
    on timers.request_id = nginx.req_id
```

---

# Самые популярные урлы страницы Цены КМ

Топ-1000 популярных запросов на странице сервиса. Полезны для анализа дата-граббером.

Теги: `тестирование`, `км`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbOBJfFtzcrh77H7aRzLYbCudziwgYUQyUzAIEdrpA=

```sql
use marketclickhouse;

select
    url as qs
from market.nginx2
where
    date = today()
    and page_id = 'market:product-offers'
    and environment = 'PRODUCTION'
    and (position(url, '&how=') > 1 or position(url, '?how=') > 1)
group by url
order by count(url) desc
limit 1000;
```

---

# JOIN трассировки и ошибок приложения

Позволяет отследить трассировки, на которых произошли ошибки. 

Помогает детально проанализировать причину возникновения ошибок в релизе.

Теги: `ошибки`, `трассировка`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbdDBJKfZcFhAEzJQxAFsv8OdABHUqXOb9GFR05dug=

```sql
USE marketclickhouse;

select
    target_module,
    request_method,
    code,
    count() as hits
from (
    select
        code,
        request_id,
        message,
        stack_trace,
        extra_keys,
        extra_values,
        substring(request_id, 1, 46) as trace_id
    from market.market_errors
    where date = toDate('2021-08-23')
    and timestamp >= toUnixTimestamp('2021-08-23 13:20:00')
    and timestamp <= toUnixTimestamp('2021-08-23 13:50:00')
    and environment = 'PRODUCTION'
    and service in ('market_front_api')
    and message = 'Timeout awaiting \'request\' for 1000ms'
    and host in (
        'man0-1821-0e6-man-market-prod-f-ba0-8041.gencfg-c.yandex.net',
        'man0-2161-man-market-prod-front-ba0-8041.gencfg-c.yandex.net',
        'vla3-1734-bb3-vla-market-prod-f-343-7478.gencfg-c.yandex.net',
        'vla3-1742-969-vla-market-prod-f-343-7478.gencfg-c.yandex.net',
    )
) as errors inner join (
    select
        id_ms,
        id_hash,
        type,
        target_module,
        request_method,
        http_code,
        query_params,
        kv_keys,
        kv_values,
        concat(toString(id_ms),  '/', id_hash) as trace_id
    from market.market_front_trace
    where date = toDate('2021-08-23')
    and timestamp >= toUnixTimestamp('2021-08-23 13:20:00')
    and timestamp <= toUnixTimestamp('2021-08-23 13:50:00')
    and environment = 'PRODUCTION'
    -- and target_module = ''
    -- and source_module = 'market_front_touch'
    and environment = 'PRODUCTION'
    and module = 'market_front_api'
    and host in (
        'man0-1821-0e6-man-market-prod-f-ba0-8041.gencfg-c.yandex.net',
        'man0-2161-man-market-prod-front-ba0-8041.gencfg-c.yandex.net',
        'vla3-1734-bb3-vla-market-prod-f-343-7478.gencfg-c.yandex.net',
        'vla3-1742-969-vla-market-prod-f-343-7478.gencfg-c.yandex.net',
    )
    and http_code != 200
) as trace
on errors.trace_id = trace.trace_id
group by target_module, request_method, code
order by hits desc;
```

---

# Анализ деградации TTLB на урлах

Запрос позволяет увидеть, на каких урлах случилась деградация TTLB.

Теги: `анализ деградации`, `ttlb`, `метрики скорости`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbTXAVK8P1EbnkK-QfRqyVH2e8wE_sAWA82vQraDu8=

```sql
use marketclickhouse;

select 
    url,

    current_p99,
    prev_p99,
    current_p99 - prev_p99 as delta_p99,

    current_hits,
    prev_hits,
    current_hits - prev_hits as delta_hits
  from (
    select
        count() as current_hits,
        quantileTiming(0.99)(resptime_ms) as current_p99,
        url
      from market.nginx2
     where (
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'
        and page_id = 'market:list'
    )
     group by url
    having current_hits > 100
     order by current_p99 desc
) as current left join (
    select
        count() as prev_hits,
        quantileTiming(0.99)(resptime_ms) as prev_p99,
        url
      from market.nginx2
     where (
        date = today()
        and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
        and environment = 'PRODUCTION'
        and page_id = 'market:list'
    )
     group by url
    having prev_hits > 100
     order by prev_p99 desc
) as previous
    on current.url = previous.url
 where prev_hits != 0
   and current_hits != 0
 order by delta_p99 desc, delta_hits desc;
```

---

# Главные превышатели 99 перцентиля TTLB

Собирает страничные данные по TTLB, грамотно собирает данные о вызове ремоут-резолверов.

Теги: `ttlb`, `resolver`, `резолвер`.

Ссылка: https://yql.yandex-team.ru/Operations/YVamJK5ODy4UJXj-9jpxfp76Yve759EaYxN7CzlzmwY=

```sql
use marketclickhouse;

select
    arrayJoin(resource) as res,
    count() as cnt
from (
    with (
        select
            count()
        from market.nginx2
        where date = today()
            and vhost = 'market.yandex.ru'
            and timestamp > now() - 3600
            and http_code = 200
            and suspiciousness = ''
            and page_id != ''
    ) as TOTAL

    select if(
        page_id = 'api:resolve', 
        arrayMap(x -> concat('resolve:', splitByChar('=', x)[2]), extractURLParameters(url)), 
        [page_id]
    ) as resource
        
    from market.nginx2
    where date = today()
        and vhost = 'market.yandex.ru'
        and timestamp > now() - 3600
        and http_code = 200
        and suspiciousness = ''
        and page_id != ''
    
    order by resptime_ms desc
    
    limit toUInt64(ceil(TOTAL * (1 - 0.99)))
)
group by res
order by cnt desc;
```

---

# Метрики скорости в разрезе по test_id

Если нужно найти деградации скорости в экспах.

Теги: `метрики скорости`, `ttr`, `tti`, `ttlb`.

Ссылка: https://yql.yandex-team.ru/Operations/YcruDJfFtwRbFhbVdIM_J6OUwxeN_E1HKXHHIlqK2p0=

```sql
USE marketclickhouse;

SELECT
    quantileTiming(0.95)(timestamp_ms - start_time_ms) as ttr,
    quantileTiming(0.95)(timestamp_ms - start_time_ms + duration_ms) as tti,

    arrayJoin(splitByChar(',', info_values[indexOf(info_keys, 'testIds')])) as "test_id",
    count(*)
FROM market.market_client_timers
WHERE 
    date = '2021-12-28'
    and timestamp >= toUnixTimestamp('2021-12-28 00:00:00')
    and timestamp <= toUnixTimestamp('2021-12-28 00:01:00') 
    AND service = 'market_front_touch'
    and name = 'page'
    and portion = 'firstScreen'
    and page_id = 'touch:index'
group by test_id
```

Более сложный запрос, который позволяет посмотреть и на TTLB.

Ссылка: https://yql.yandex-team.ru/Operations/YUhbwgVK8HLJX9EEr8g77zXzN_agQIYPzfhNW-90HOo=

```sql
use marketclickhouse;

select
    page_id,
    test_id,
    quantileTiming(0.99)(request_TTLB) as TTLB99,
    quantileTiming(0.95)(request_TTR) as TTR95,
    quantileTiming(0.95)(request_TTI) as TTI95,
    count() as cnt
from (
    select
        request_id,
        timestamp,
        host,
        service,
        page_id,
        request_TTLB,
        request_TTR,
        request_TTI,
        test_id
    from (
        select
            timestamp,
            page_id,
            service,
            timestamp_ms - start_time_ms as request_TTR,
            timestamp_ms - start_time_ms + duration_ms as request_TTI,
            request_id
        from `market`.`market_client_timers`
        where date = toDate('2021-09-20')
        and service in ('market_front_desktop', 'market_front_touch')
        and timestamp > toUnixTimestamp('2021-09-20 11:00:00')
        and timestamp < toUnixTimestamp('2021-09-20 12:00:00')
        and name = 'page'
        and portion = 'firstScreen'
        and request_id != ''
        and page_id in ('market:index', 'touch:index')
    ) as client_timers inner join (
        select
            host,
            req_id as request_id,
            resptime_ms as request_TTLB,
            if(empty(test_id), [0], test_id) as test_id
        from market.nginx2
        where date = toDate('2021-09-20')
        and timestamp > toUnixTimestamp('2021-09-20 11:00:00')
        and timestamp < toUnixTimestamp('2021-09-20 12:00:00')
        and environment = 'PRODUCTION'
        and service in ('desktop', 'touch')
        and req_id != ''
        and resptime_ms != 0
    ) as server_timers
    on client_timers.request_id = server_timers.request_id
)
array join test_id
group by page_id, test_id
order by page_id, TTLB99 desc;
```
---

# Метрика TTR с динамикой по времени

Строит список ВРЕМЯ - TTR с интервалом в пять минут.

Теги: `метрики скорости`, `ttr`.

Ссылка: https://yql.yandex-team.ru/Operations/YVaq8ZfFtzcrh6ZF76uSi9nAyeZZDNFEAr5XgBSUL7k=

```sql
use marketclickhouse;

select
    toStartOfFiveMinute(toDateTime(timestamp)) as time,
    quantileTimingIf(0.95)(timestamp_ms - start_time_ms, portion = 'firstScreen') as TTR

from market.market_client_timers
where date = today()
    and vhost = 'market.yandex.ru'
    and timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())

group by time
order by time asc;
```

---

# Частота попадания виджета на первый экран

Сравнение частоты попадания и непопадания виджета на первый экран.

Теги: `виджет`, `первый экран`.

Ссылка: https://yql.yandex-team.ru/Operations/YVbW0wVK8P1EbnvA6A5-FQifb_PRqQrS_NE_6MmxMBc=

```sql
use marketclickhouse;

select
    widget_name,
    widget_id,
    sum(value) as result,
    sum(hits) as common_hits,
    groupArray(value),
    groupArray(hits)
  from (
      select
        service,
        page_id,
        widget_name,
        widget_id,
        on_first_screen,
        if(on_first_screen == 'true', 1, -1) * count(*) as value,
        count(*) as hits
    from (
        select
            *,
            info_values[indexOf(info_keys, 'widgetName')] as widget_name,
            info_values[indexOf(info_keys, 'widgetId')] as widget_id,
            info_values[indexOf(info_keys, 'onFirstScreen')] as on_first_screen,
            info_values[indexOf(info_keys, 'expFlags')] as exp_flags
        from `market`.`market_client_timers`
        where
            date between toDate(now() - interval '2' DAY) and toDate(now())
            and page_id = 'market:index'
            and service = 'market_front_desktop'
            and name = 'widget'
    )
    group by service, page_id, widget_name, widget_id, on_first_screen
  )
  group by service, page_id, widget_name, widget_id;
```
