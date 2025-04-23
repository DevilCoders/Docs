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
