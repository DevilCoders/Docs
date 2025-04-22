# SCOperationsImportExecutor

### Код

За работы джобы отвечает класс:
[`ru.yandex.market.billing.sortingcenter.SCBillingExecutor`](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/sortingcenter/SCBillingExecutor.java?rev=4f384e170a#L19)

### Продукт/подсистема


Биллинг логистики


### Роль в работе продукта/подсистемы

Джоба агрегирует и импортирует данные по операциям сортировочных центров из YT


### Датафлоу

Джоба читает данные из табличек в постгресе:

market_billing.sc_tariff
market_billing.sc_tariff_min
market_billing.sc_operation

Джоба пишет данные в таблички постгреса:

market_billing.sc_operation_cost

### Способы наблюдения за текущим состоянием
Чтобы понять, есть ли обиллные занчения за сегодня можно проверить содержание таблички :

```postgresql
select *
from market_billing.sc_operation_cost
where date_trunc('day', sorting_date)::date = current_date - 1;
```

Проверить лог кварца по имени джобы:
```postgresql
select *
from public.qrtz_log
where job_name = 'scBillingExecutor'
order by trigger_fire_time desc
limit 10;
```
Также можно проверить флаги в env на которые смотрит джоба:

Запущен ли биллинг СЦ: `market.billing.sorting_center.is_enabled`<br>
Дата с которой будет биллится при следующем запуске: `market.billing.sorting_center.billing.start_date`

Запросом:
```postgresql
select value
from shops_web.environment
where name = :name;
```

### Какая функциональность пострадает от отказа джобы

Джоба является частью биллинга сортировочных центров. Джоба занимается непосредственно биллингом действий СЦ.

### Как пользователи (или команда) заметят проблему и через какое время

Биллинг не произойдёт, сортировочные центры не получат выплат.

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
Для переобилливания прошедших периодов можно подергать этот флаг
```postgresql
select value
from shops_web.environment
where name = 'market.billing.sorting_center.billing.start_date';
```
### Известные причины поломок

На текущий момент нет таких

### Дополнительно: тонкости и подводные камни

