## Полная сверка отчетов по реализации товаров

Скрипт работает в трёх режимах
1. Получить id поставщиков по данным отчётов в MDS (если они там есть) - метод get_supplier_list()
2. Сравнить отчёты для выбранных поставщиков (id поставщиков должны быть в файле suppliers.id.list) - метод compare_reports()
3. Сравнить отчёты для одного поставщика - метод compare_report(id)

## Пример использования

Получить список id поставщиков, например запросом в базу


```
with orders as (
     (select order_id
     from market_billing.cpa_order_status_history
     where TRANTIME >= :startDate
       and trantime < :endDate
     union all
     select ORDER_ID
     from market_billing.v_supplier_resupply res
     where res.created_at >= :startDate
       and res.created_at < :endDate)
)
select distinct(coi.FF_SUPPLIER_ID) from market_billing.CPA_ORDER_ITEM coi
    join orders o on coi.order_id = o.order_id
order by FF_SUPPLIER_ID;
```

Поместить выбранные Id в файл suppliers.id.list

При необходимости поправить шаблоны путей до отчётов в MDS

Запустить скрипт с раскомментированым вызовом метода compare_reports()

В результате работы скрипта будет создана папка failed, в которой будут сложены отчёты поставщиков, данные в которых не совпадают, а также файл с общей информацией о несовпадениях
например

```
1000012.xlsx
1000012_report.txt
1000012_YT.xlsx
```

Также скрипт выведет текущую и итоговую статистику по расхождениям 
