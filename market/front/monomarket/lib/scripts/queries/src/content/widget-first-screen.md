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
