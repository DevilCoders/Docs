## SyncMarketFeedsJob

### Продукт/подсистема

Интеграция с Единым офферным хранилищем.

Оффер - некоторый товар в интернет-магазине. </br>
Фид - сущность, содержащая в себе информацию, как получить список товаров для генерации в Баннерленде смарт-баннеров и динамических объявлений. Мета-информация о фиде в Директе хранится в таблице [ppc.feeds](https://direct-dev.yandex-team.ru/db/ppc/tables/feeds.html).


### Роль в работе продукта/подсистемы

Загружает мета-информацию по фидам из Маркета в таблицу [ppc.feeds](https://direct-dev.yandex-team.ru/db/ppc/tables/feeds.html).


### Датафлоу

- Данные берутся из таблицы [//home/market/production/ecom/export/clients/recent](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/ecom/export/clients/recent). При включенной фиче `SYNC_MARKET_FEEDS_BY_SHOP_ID` фиды объединяются в один по `shop_id`.
- Результаты складываются в таблицу [ppc.feeds](https://direct-dev.yandex-team.ru/db/ppc/tables/feeds.html).
- Так же заполняется поле `market_business_id` в [ppc.clients_options](https://direct-dev.yandex-team.ru/db/ppc/tables/clients_options.html)
- При удалении фида из Маркета, если есть активные группы с этим фидом, то для смартов и ДО они останавливаются, а из ТГО фид удаляется

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.SyncMarketFeedsJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'service~'method~'span_id~'message)~conditions~(service~'direct.jobs~method~'marketfeeds.SyncMarketFeedsJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [Solomon мониторинги](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs-push&service=push-monitoring&l.flow=SyncMarketFeedsJob&l.env=production&l.host=CLUSTER&graph=auto&stack=false&downsamplingFill=none&secondaryGraphMode=bars&b=4d&e=)

### Какая функциональность пострадает от отказа джобы

Фиды перестанут синхронизироваться с Маркетом.


### Как пользователи (или команда) заметят проблему и через какое время

Начнут жаловаться, что загрузили фид в Маркет, а в Директе его не видят. Могут воспользоваться воркэраундом и загрузить фид в Директ вручную.


### Контакты разработчиков и менеджеров

Разработчики: [Сергей Ковач](https://staff.yandex-team.ru/buhter), [Дмитрий Анощенков](https://staff.yandex-team.ru/dmitanosh) <br/>
Менеджеры: [Дмитрий Уляшев](https://staff.yandex-team.ru/ulyashevda)


### Желательное время исправления в случае поломки

Дни, т.к. поломка джобы не создаст для пользователей непреодолимых проблем. Но, по мере устаревания данных, пользователям придётся совершать больше действий для запуска рекламы.


### Способы регулирования работы джобы

Фича `SYNC_MARKET_FEEDS_BY_SHOP_ID` определяет, нужно ли выгружать из yt фиды по `market_feed_id` или по `market_shop_id`.


### Известные причины поломок

До исправления [DIRECT-137739](https://st.yandex-team.ru/DIRECT-137739) джоба перестаёт работать при недоступности HAHN.


### Дополнительно: тонкости и подводные камни
