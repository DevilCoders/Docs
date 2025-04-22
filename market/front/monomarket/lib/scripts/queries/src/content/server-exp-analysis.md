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
