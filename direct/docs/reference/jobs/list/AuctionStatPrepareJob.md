## AuctionStatPrepareJob

### Продукт/подсистема

Статистика работы фразы на поисковых площадках.


### Роль в работе продукта/подсистемы

Первый этап загрузки из БК статистики по фразам на поисковых площадках. Достаточно общая функциональность, используется во многих местах (в том числе обратно передается в торги).

Второй этап - джоба [AuctionStatUpdateJob](AuctionStatUpdateJob.md) - пользуется результатами данной джобы.


### Датафлоу

- С помощью [yql запроса](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/statistics/auctionstat/prepare.yql) загружает статистику по фразам из одного из кластеров, указанных в [app-production.conf приложения jobs](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/app-production.conf) в секции `yt/mapreduce_clusters`.
- Используемая в запросе таблица в БК: [//home/yabs/stat/BannerPhraseStatControl](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/stat/BannerPhraseStatControl). Запрос выполняется на том кластере, на котором атрибут таблицы `last_sync_time_bs-chevent-log` имеет большее значение и больше, чем при предыдущем запуске.
- Результат складывает в таблицу [//home/direct/import/auctionstat/prepared_data](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/import/auctionstat/prepared_data). У таблицы проставляет атрибут `last_sync_time_bs-chevent-log` равный соответствующему атрибуту таблицы БК.


### Способы наблюдения за текущим состоянием

- [График](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.env=production&l.sensor=bs_auction_stat_updated_rows&graph=auto&stack=false&transform=differentiate&b=2021-03-21T16%3A37%3A40.613Z&e=2021-03-22T16%3A37%3A40.613Z) количества обновленных в mysql строк (продифференцирован).
- Ppc-property `AUCTIONSTAT_PREPARED_CHEVENT_TIME` хранит значение атрибута таблицы `last_sync_time_bs-chevent-log` на момент последнего успешного чтения.
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.AuctionStatPrepareJob.working.production&query=&last=1DAY) - если на всех кластерах отставание больше 7 часов, загорится мониторинг.
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'auctionstat.AuctionStatPrepareJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


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
