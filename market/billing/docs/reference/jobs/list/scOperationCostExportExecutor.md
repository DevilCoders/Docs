# SCOperationsImportExecutor

### Код

За работы джобы отвечает класс:
`ru.yandex.market.billing.sortingcenter.SCOperationCostExportExecutor`

### Продукт/подсистема

Биллинг логистики

### Роль в работе продукта/подсистемы

Джоба выгружает обиллиные данные в YT

### Датафлоу

Джоба читает данные из таблички в PG:

`market_billing.sc_operation_cost`

Пишет в папку на YT:

Целевая папка указывается переменной окружения:
`market.billing.sorting_center.export.target_folder`

### Способы наблюдения за текущим состоянием
Чтобы понять, был-ли сегодня успешный импорт данных можно проверить наличие актуальных данных за вчерашний день:
Джоба берет данные из таблички в PG и кладет их в YT. Поэтому для проверки работы джобы можно

1) Проверить лог кварца по имени джобы:
```postgresql
select *
from public.qrtz_log
where job_name = 'scOperationsImportExecutor'
order by trigger_fire_time desc
limit 10;
```
2) Проверить есть ли значения в PG
```postgresql
select count(*)
from market_billing.sc_operation_cost
where date_trunc('day', sorting_date)::date = current_date - 1;
```
3) Проверить наличие/значения таблички в YT по пути записанном в переменной окружения по ключу `market.billing.sorting_center.export.target_folder`


4) Также можно проверить флаги в env на которые смотрит джоба:
    - запущен ли биллинг СЦ: `market.billing.sorting_center.is_enabled`<br>
    - дата с которой будет биллится при следующем запуске: `market.billing.sorting_center.export.start_date`

    Запросом:
    ```postgresql
    select value
    from shops_web.environment
    where name = :name;
    ```

### Какая функциональность пострадает от отказа джобы

Джоба является частью биллинга сортировочных центров. Если информация об обиллиных операциях сортировочных центров не будет выгружена в YT, эти значения не попадут в табличку с обиллиными данными. И мы не сможем выплатить партнерам деньги за проведенные операции.

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
Переменная в env указывающая на дату экспорта:
```
market.billing.sorting_center.export.start_date
```
### Известные причины поломок

На текущий момент нет таких

### Дополнительно: тонкости и подводные камни

