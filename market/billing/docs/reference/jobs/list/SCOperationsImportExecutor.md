# SCOperationsImportExecutor

### Код

За работы джобы отвечает класс:
`ru.yandex.market.billing.imports.sortingcenter.SCOperationsImportExecutor`

### Продукт/подсистема


Биллинг логистики


### Роль в работе продукта/подсистемы

Джоба агрегирует и мпортирует данные по операция сортировочных центров из YT


### Датафлоу

Джоба читает данные из YT табличек на 'Хане':

`hahn.'//home/market/production/tpl/sc/cdc/place_history'`
`hahn.'//home/market/production/tpl/sc/cdc/sorting_center'`
`hahn.'//home/market/production/tpl/sc/cdc/place'`
`hahn.'//home/market/production/tpl/sc/cdc/measurements'`
`hahn.'//home/market/production/tpl/sc/cdc/orders'`
`hahn.'//home/market/production/tpl/sc/cdc/order_ff_status_history'`

Пишет в табличку на ТМС постгресе:

`market_billing.sc_operation`

### Способы наблюдения за текущим состоянием
Чтобы понять, был-ли сегодня успешный импорт данных можно проверить наличие актуальных данных за вчерашний день:

```postgresql
select count(*)
from market_billing.sc_operation
where date_trunc('day', sorting_date)::date = current_date - 1;
```

Проверить лог кварца по имени джобы:
```postgresql
select *
from public.qrtz_log
where job_name = 'scOperationsImportExecutor'
order by trigger_fire_time desc
limit 10;
```
Также можно проверить флаги в env на которые смотрит джоба:

запущен ли биллинг СЦ: `market.billing.sorting_center.is_enabled`<br>
дата с которой будет биллится при следующем запуске: `market.billing.sorting_center.import.start_date`

Запросом:
```postgresql
select value
from shops_web.environment
where name = :name;
```

### Какая функциональность пострадает от отказа джобы

Джоба является частью биллинга сортировочных центров. Если информация об операциях сортировочных центров не будет выгружена в ПГ, они не будут обиллины за эти дни.

### Как пользователи (или команда) заметят проблему и через какое время

Биллинг не произойдёт, сортировочные центры не получат выплат

### Контакты разработчиков и менеджеров

Разработчики: [Кирилл Матвеев(makivay)](https://staff.yandex-team.ru/makivay), [Андрей Быстров(andreybystrov)](https://staff.yandex-team.ru/andreybystrov) <br/>
Менеджеры: [Софина Чамрон(schamron)](https://staff.yandex-team.ru/schamron)

### Желательное время исправления в случае поломки



### Способы регулирования работы джобы

Джоба подчиняется общему для биллинга сц флагу:
```postgresql
select value
from shops_web.environment
where name = 'market.billing.sorting_center.is_enabled';
```

### Известные причины поломок

На текущий момент нет таких

### Дополнительно: тонкости и подводные камни

