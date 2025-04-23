# Список алертов и способов их заведения
## Алерты на количество групп gencfg
Алерты заведены с помощью шаблонизатора-обновлятора **infra/rtc/golovan**.
* infra/rtc/golovan/alerts/templated/hostman_gencfg_groups_count_prestable - хосты из QLOUD, ASEARCH c ctype=prestable
* infra/rtc/golovan/alerts/templated/hostman_gencfg_groups_count_production - хосты из QLOUD, ASEARCH c ctype=production


## Алерты на количество неудачных отправок node_info
Алерты заведены с помощью шаблонизатора-обновлятора **infra/rtc/golovan**.
* infra/rtc/golovan/alerts/templated/hostman_nodeinfo - хосты из QLOUD, ASEARCH

## Типичный workflow для работы с шаблонизатором
* поправили шаблон алерта
* запустили infra/rtc/golovan/updater --dry-run
* убедились, что алерты отрендерились как надо
* запустили infra/rtc/golovan/updater - он применит все алерты в головане
* закоммитили измененные шаблоны
