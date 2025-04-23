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
