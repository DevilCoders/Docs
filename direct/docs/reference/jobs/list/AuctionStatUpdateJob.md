## AuctionStatUpdateJob

### Продукт/подсистема

Статистика работы фразы на поисковых площадках.


### Роль в работе продукта/подсистемы

Второй этап загрузки из БК статистики по фразам на поисковых площадках.  Достаточно общая функциональность, используется во многих местах (в том числе обратно передается в торги).

Записывает статистику, подготовленную джобой [AuctionStatPrepareJob](AuctionStatPrepareJob.md), в таблицу [ppc.bs_auction_stat](https://direct-dev.yandex-team.ru/db/ppc/tables/bs_auction_stat.html).


### Датафлоу

Шардированная джоба.

- Для каждого шарда с помощью операции `merge` отбирает из созданной `AuctionStatPrepareJob` таблицы только те строки, у которых поле шард равно номеру шарда.
- Складывает данные в таблицу [//home/direct/import/auctionstat/prepared_data_<shard>](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/direct/import/auctionstat).
- Выполняется на том кластере, на котором у исходной таблицы больше атрибут `last_sync_time_bs-chevent-log`, но не меньше, чем при прошлом запуске.
- Читает полученную таблицу `//home/direct/import/auctionstat/prepared_data_<shard>`  и обновляет [ppc.bs_auction_stat](https://direct-dev.yandex-team.ru/db/ppc/tables/bs_auction_stat.html).


### Способы наблюдения за текущим состоянием

- Ppc-property `auctionstat_update_chevent_log_timestamp_SHARD_<N>` - хранит значение атрибута `last_sync_time_bs-chevent-log` исходной таблицы на момент последнего успешного чтения.
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.AuctionStatUpdateJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'auctionstat.AuctionStatUpdateJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Получение статистики по фразам из БК. Таблица [ppc.bs_auction_stat](https://direct-dev.yandex-team.ru/db/ppc/tables/bs_auction_stat.html) используется очень глубоко и во многих местах (в том числе обратно передается в торги). С одной стороны, в описании таблицы написано, что свежесть и правильность данных [не гарантируется](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/db_schema/ppc/bs_auction_stat.text?rev=r5741315#L5)), а с другой - не известно что и как на неё завязано.


### Как пользователи (или команда) заметят проблему и через какое время

Не известно.


### Контакты разработчиков и менеджеров

Разработчики: [Марина Спиридонова](https://staff.yandex-team.ru/mspirit), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

1 - 2 дня.


### Способы регулирования работы джобы




### Известные причины поломок

Отставание таблиц БК


### Дополнительно: тонкости и подводные камни
