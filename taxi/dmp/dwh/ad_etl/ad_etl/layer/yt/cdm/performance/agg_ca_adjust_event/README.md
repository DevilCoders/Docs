См. TAXIDWH-14096

Для части событий Adjust (события с event_type = 'succes_order') логика проставления moscow_dt отличается от остальных.
Поэтому была реализована схема, приведенная ниже:
```
 eventlog -----> wo_success_order --------+
    |                                     |
    |                                     +-> agg_ca_adjust_event
    ↓                                     |
success_order_log ---> w_success_order ---+
```

__success_order_log__ - события из eventlog с условием event_type = 'success_order' \
__agg_ca_adjust_event_success_order__ заполняется из success_order_log с измененной логикой moscow_dt \
__agg_ca_adjust_event_wo_success_order__ заполняется из eventlog с фильтром на event_type != 'success_order' \
итоговая таблица __agg_ca_adjust_event__ является объединением agg_ca_adjust_event_wo_success_order и agg_ca_adjust_event_success_order