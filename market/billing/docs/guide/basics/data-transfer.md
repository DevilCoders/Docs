# Настройка копирования и репликации данных с использованием Data Transfer

Общая документация про Data Transfer для внешнего облака находится [здесь](https://docs.yandex-team.ru/cloud/data-transfer/)
В ней описаны основные концепции, принципы использования, источники и приёмники, за исключением YT.

## Настройка репликации таблиц из Postgresql в YT

Порядок заведения репликации из Postgresql в YT при помощи Data Transfer (DT)

1 Завести пользователя, под которым будет проходить доступ в базу Postgresql от DT.

Пользователя могут завести пользователи с ролью [администраторы БД](https://abc.yandex-team.ru/services/market_billing/?scope=db_management).
Необходимо, чтобы у робота кроме права на чтение, было право для репликации `mdb_replication`.

В проде пользователь `data_transfer`, в тестовой бд - `data_transfer_testing`.
Список пользователей доступен через UI: [прод](https://yc.yandex-team.ru/folders/foofljs7dr5uhp54fh22/managed-postgresql/cluster/mdbke58al8r4k1jj1qn7?section=users),
и [тестинг](https://yc.yandex-team.ru/folders/foofljs7dr5uhp54fh22/managed-postgresql/cluster/mdbger39ogj8q5aagbjl?section=users).
Пароли: [для тестинга](https://yav.yandex-team.ru/secret/sec-01fs7fyrgxvem1bpdcgt37ywam), [для прода](https://yav.yandex-team.ru/secret/sec-01fy3qsqgbbhhckgjz043d1s38)

2 Выбрать (создать) путь в YT, в который планируется проведение репликации.

Для этого пути добавить права для робота `@robot-lf-dyn-push` на `use` аккаунта, к которому относится путь (`market-mbi-development`, `market-billing-testing` и т.д.) и на `mount`, `read`, `read and write` для самого пути.
Сформировать запросы на получение прав можно через вкладку `ACL` для пути в YT, далее `Request permissions`

![UI запроса прав](_assets/data_transfer_acl.png "" =1200x300)

Пример запросов прав через IDM
[use](https://idm.yandex-team.ru/system/yt-cluster-hahn/roles#f-status=all,f-role=yt-cluster-hahn,sort-by=-updated,role=56145782), [mount](https://idm.yandex-team.ru/system/yt-cluster-hahn/roles#f-status=all,f-role=yt-cluster-hahn,sort-by=-updated,role=56145783),
[read](https://idm.yandex-team.ru/system/yt-cluster-hahn/roles#f-status=all,f-role=yt-cluster-hahn,sort-by=-updated,role=56145784), [read and write](https://idm.yandex-team.ru/system/yt-cluster-hahn/roles#f-status=all,f-role=yt-cluster-hahn,sort-by=-updated,role=56145785)

3 Создать новый источник для таблиц из Postgresql, или добавить новые таблицы в существующий

[Пример источника](https://yc.yandex-team.ru/folders/foofljs7dr5uhp54fh22/data-transfer/endpoint/dtencb6foevi600a3e55/view)
Необходимое условие для репликации таблицы - наличие в ней первичного ключа.

4 Создать новый приёмник в YT.

[Пример приёмника](https://yc.yandex-team.ru/folders/foofljs7dr5uhp54fh22/data-transfer/endpoint/dtefmil1v5hnggsg6qsf/view)

Квота на динамические таблицы в YT берётся из аккаунта (задаётся настройками `Tablet cell bundle for quota accounting`). Для тестовых случаев можно использовать коммунальные (`cdc`)
Хранилище данных (ssd или hdd) задаётся параметром `Where to store data (YT Medium)` - варианты `ssd_blobs/default`

5 После этого нужно создать трансфер из источника в приёмник.

[Пример трансфера](https://yc.yandex-team.ru/folders/foofljs7dr5uhp54fh22/data-transfer/transfer/dttdchju61498k68l7v8/view)

Типы трансфера описаны [тут](https://docs.yandex-team.ru/cloud/data-transfer/concepts/#transfer-type)

6 Для начала копирования или репликации данных активировать трансфер.

В UI это делается кнопкой `Активировать` в панели трансфера.
Текущее состояние трансфера можно отслеживать по мониторингам в [solomon](https://solomon.yandex-team.ru/?project=data-transfer&cluster=rtc-prod&dashboard=transfer_dashboard&l.resource_id=dttdchju61498k68l7v8&l.source_type=pg&l.target_type=yt&l.source_id=mdbger39ogj8q5aagbjl&l.target_id=hahn--home-market-development-mbi-billing-pg-replication&b=1h&job_index=*)

{% note info %}

По выбранному пути приёмника в YT каждая таблица из Postgresql складывается в свою динамическую таблицу.
Именование таблицы - `имя_схемы(БД)_имя_таблицы`, например в таблица `market_billing.cpa_order` из Postgresql будет складываться в YT как `market_billing_cpa_order`

{% endnote %}

{% note info %}

Если в настройках приёмника YT включен параметр `Хранить ли удаления в отдельной архивированной таблице`, то удаленные из Postgresql значения будут переноситься в YT в отдельную таблицу рядом с основной с суффиксом `_archive` (`market_billing_cpa_order_archived`).
Кроме самих данных в неё добавляется время транзакции.

{% endnote %}

