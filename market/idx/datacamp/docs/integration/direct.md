## Общая схема интеграции

Для регистрации в маркетном пространстве партнеров (получения `business_id, shop_id, feed_id`) используется MBI. Каналы поставки офферов отличаются в зависимости от продукта директа

### Дикий веб
В эту категорию попадают продукты **"смарт по сайту"** и **"превью по сайту"**. Суть в том, что рекламодатель заносит в директ сайт, а директ сам парсит оттуда офферы и генерирует баннеры. Превью отличается тем, что директ сам генерирует небольшой сэмпл по сайту и делает мерчу демку того, как мог бы выглядить подключенный "смарт"
![direct-wild](../_images/direct-wild.png)

### Фиды
Продукт **"динамические объявления"** - основной бизнес РСЯ, в котором партнеры приносят фиды, а директ генерирует по ним баннеры
![direct-feed](../_images/direct-feed.png)

## Цвет офферов Директа в DataCamp

    DIRECT = 6; - //deprecated// (Устаревший общий признак Директа, включающий в себя все пайплайны)
    DIRECT_SITE_PREVIEW = 9; (Превью по сайту, без подключения и регистрации)
    DIRECT_STANDBY = 10; (Превью по фиду)
    DIRECT_GOODS_ADS = 11; (Динамические объявления и Смартбаннеры = ДО и Смарты)
    DIRECT_SEARCH_SNIPPET_GALLERY = 12; - //deprecated// (Текстово-графические объявления = ТГО)

## Удаление офферов
Удаление офферов выполняет [DataCamp Cleaner](../components/routines/cleaner.md)
SB scheduler - [https://sandbox.yandex-team.ru/scheduler/698967/view](https://sandbox.yandex-team.ru/scheduler/698967/view)

Удаление офферов происходит по ttl согласно стратегиям. Для Директа существуют 3 стратегии удаления ([proto](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/common/RemoveStrategy.proto?rev=r8992107#L31-36 )):
1. DIRECT_DISABLED_BY_PARTNER_FEED: Удаляем сервисные офферы скрытые фидом. TTL = 1w.
2. DIRECT_DISABLED_BY_PARTNER_SITE: Удаляем скрытые сервисные офферы дикого веба. TTL = 1w.
3. DIRECT_SHOP_DISABLED: Удаляем сервисные офферы для выключенных в [таблице партнеров](https://yt.yandex-team.ru/arnold/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/united/partners). Ts скрытия магазина - [disabled_since_ts](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/tables/Partner.proto#L22). TTL = 1d.

Базовые части офферов удаляются при отсутствие сервисных согласно стратегии NO_SERVICE. TTL = 1w с момента создания оффера.
При первом обходе Cleaner проставляет офферам флаг [removed](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r9004475#L238) и [remove_strategy](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r9004475#L251), при последующем запуске удаляет сами офферы.

## Метрики

### Количество офферов Директа в DataCamp
[График](https://monitoring.yandex-team.ru/projects/datacamp/explorer?normz=off&colors=auto&type=line&interpolation=linear&dsp_method=auto&dsp_aggr=last&dsp_interval=300000&dsp_fill=previous&vis_labels=off&vis_aggr=avg&q.0.text=%7Bproject%3D%22market.datacamp%22%2C%20service%3D%22routines%22%2C%20sensor%3D%22offers_count%7Coffers_count_wild_web%22%2C%20cluster%3D%22production%22%2C%20stats_type%3D%22inner_state_direct%22%7D&from=1658070626590&to=1658675426590)

### Первая картинка
Для отправки оффера в топики Bannerland оффер должен получить первую картинку от Picrobot. Для определения версии первой картинки используется отдельное поле [bannerland_picture_version](https://a.yandex-team.ru/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r9512152#L278).

Графики время прокачки первой картинки:
- Метрика с детализацией времени по офферам **за все время** [график](https://monitoring.yandex-team.ru/projects/datacamp/explorer?legend.offers_direct_processing_24h_or_more.name=%D0%B1%D0%BE%D0%BB%D1%8C%D1%88%D0%B5%20%D1%81%D1%83%D1%82%D0%BE%D0%BA&legend.offers_direct_processing_24h_or_more.color=cc0000&legend.offers_direct_processing_1h_to_2h.name=%D0%BE%D1%82%20%D1%87%D0%B0%D1%81%D0%B0%20%D0%B4%D0%BE%20%D0%B4%D0%B2%D1%83%D1%85&legend.offers_direct_processing_1h_to_2h.color=99ff99&legend.offers_direct_processing_2h_to_24h.name=%D0%BE%D1%82%20%D0%B4%D0%B2%D1%83%D1%85%20%D1%87%D0%B0%D1%81%D0%BE%D0%B2%20%D0%B4%D0%BE%20%D1%81%D1%83%D1%82%D0%BE%D0%BA&legend.offers_direct_processing_2h_to_24h.color=ea9999&legend.offers_direct_processing_1h_or_less.name=%D0%BC%D0%B5%D0%BD%D1%8C%D1%88%D0%B5%20%D1%87%D0%B0%D1%81%D0%B0&legend.offers_direct_processing_1h_or_less.color=32ff32&legend.3600%7Cfirst_picture_histo.name=less%20than%201h&legend.3600%7Cfirst_picture_no_avatar_histo.name=%28no%20avatar%29%20less%20than%201h&legend.21600%7Cfirst_picture_histo.name=1h%20-%206h&legend.21600%7Cfirst_picture_no_avatar_histo.name=%28no%20avatar%29%201h%20-%206h&legend.43200%7Cfirst_picture_histo.name=6h%20-%2012h&legend.43200%7Cfirst_picture_no_avatar_histo.name=%28no%20avatar%29%206h%20-%2012h&legend.86400%7Cfirst_picture_histo.name=12h%20-%201d&legend.86400%7Cfirst_picture_no_avatar_histo.name=%28no%20avatar%29%2012h%20-%201d&legend.172800%7Cfirst_picture_histo.name=1d%20-%202d&legend.172800%7Cfirst_picture_no_avatar_histo.name=%28no%20avatar%29%201d%20-%202d&legend.345600%7Cfirst_picture_histo.name=2d%20-%204d&legend.345600%7Cfirst_picture_no_avatar_histo.name=%28no%20avatar%29%202d%20-%204d&legend.604800%7Cfirst_picture_histo.name=4d%20-%201w&legend.604800%7Cfirst_picture_no_avatar_histo.name=%28no%20avatar%29%204d%20-%201w&legend.1209600%7Cfirst_picture_histo.name=1w%20-%202w&legend.1209600%7Cfirst_picture_no_avatar_histo.name=%28no%20avatar%29%201w%20-%202w&legend.2419200%7Cfirst_picture_histo.name=2w%20-%204w&legend.2419200%7Cfirst_picture_no_avatar_histo.name=%28no%20avatar%29%202w%20-%204w&normz=on&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg&q.0.s=%7Bproject%3D%22market.datacamp%22%2C%20cluster%3D%22production%22%2C%20service%3D%22routines%22%2C%20stats_type%3D%22ecom_export_direct%22%2C%20sensor%3D%22first_picture_no_avatar_histo%7Cfirst_picture_histo%22%7D&q.0.ct=auto&from=now-1w&to=now) ([график до 22 июня](https://nda.ya.ru/t/DUTINlFm59GgjL))
- Метрика с детализацией времени по офферам  **за последнюю неделю** [график](https://monitoring.yandex-team.ru/projects/datacamp/explorer?legend.offers_direct_processing_24h_or_more.name=%D0%B1%D0%BE%D0%BB%D1%8C%D1%88%D0%B5%20%D1%81%D1%83%D1%82%D0%BE%D0%BA&legend.offers_direct_processing_24h_or_more.color=cc0000&legend.offers_direct_processing_1h_to_2h.name=%D0%BE%D1%82%20%D1%87%D0%B0%D1%81%D0%B0%20%D0%B4%D0%BE%20%D0%B4%D0%B2%D1%83%D1%85&legend.offers_direct_processing_1h_to_2h.color=99ff99&legend.offers_direct_processing_2h_to_24h.name=%D0%BE%D1%82%20%D0%B4%D0%B2%D1%83%D1%85%20%D1%87%D0%B0%D1%81%D0%BE%D0%B2%20%D0%B4%D0%BE%20%D1%81%D1%83%D1%82%D0%BE%D0%BA&legend.offers_direct_processing_2h_to_24h.color=ea9999&legend.offers_direct_processing_1h_or_less.name=%D0%BC%D0%B5%D0%BD%D1%8C%D1%88%D0%B5%20%D1%87%D0%B0%D1%81%D0%B0&legend.offers_direct_processing_1h_or_less.color=32ff32&legend.3600%7Cfirst_picture_rolling_1w_histo.name=less%20than%201h&legend.3600%7Cfirst_picture_rolling_1w_no_avatar_histo.name=%28no%20avatar%29%20less%20than%201h&legend.21600%7Cfirst_picture_rolling_1w_histo.name=1h%20-%206h&legend.21600%7Cfirst_picture_rolling_1w_no_avatar_histo.name=%28no%20avatar%29%201h%20-%206h&legend.43200%7Cfirst_picture_rolling_1w_histo.name=6h%20-%2012h&legend.43200%7Cfirst_picture_rolling_1w_no_avatar_histo.name=%28no%20avatar%29%206h%20-%2012h&legend.86400%7Cfirst_picture_rolling_1w_histo.name=12h%20-%201d&legend.86400%7Cfirst_picture_rolling_1w_no_avatar_histo.name=%28no%20avatar%29%2012h%20-%201d&legend.172800%7Cfirst_picture_rolling_1w_histo.name=1d%20-%202d&legend.172800%7Cfirst_picture_rolling_1w_no_avatar_histo.name=%28no%20avatar%29%201d%20-%202d&legend.345600%7Cfirst_picture_rolling_1w_histo.name=2d%20-%204d&legend.345600%7Cfirst_picture_rolling_1w_no_avatar_histo.name=%28no%20avatar%29%202d%20-%204d&legend.604800%7Cfirst_picture_rolling_1w_histo.name=4d%20-%201w&legend.604800%7Cfirst_picture_rolling_1w_no_avatar_histo.name=%28no%20avatar%29%204d%20-%201w&legend.1209600%7Cfirst_picture_rolling_1w_histo.name=1w%20-%202w&legend.1209600%7Cfirst_picture_rolling_1w_no_avatar_histo.name=%28no%20avatar%29%201w%20-%202w&legend.2419200%7Cfirst_picture_rolling_1w_histo.name=2w%20-%204w&legend.2419200%7Cfirst_picture_rolling_1w_no_avatar_histo.name=%28no%20avatar%29%202w%20-%204w&normz=on&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg&q.0.s=%7Bproject%3D%22market.datacamp%22%2C%20cluster%3D%22production%22%2C%20service%3D%22routines%22%2C%20stats_type%3D%22ecom_export_direct%22%2C%20sensor%3D%22first_picture_rolling_1w_no_avatar_histo%7Cfirst_picture_rolling_1w_histo%22%7D&q.0.ct=auto&from=now-1w&to=now) ([график до 22 июня](https://nda.ya.ru/t/5jPlCaKU59Ggxa))

## Потоки данных
### Входящие
#### RTHub LB топик
   Офферы Дикого Веба, прокачанные Самоваром, приходят из топиков от rthub.

   Name| Env| Link| Logs| Logs YQL
   :--- | :--- | :--- | :--- | :---
   rthub/prod/datacamp-offers| production| [link](https://lb.yandex-team.ru/logbroker/accounts/rthub/prod/datacamp-offers)| [logs](https://yt.yandex-team.ru/arnold/navigation?path=//logs/rthub-datacamp-offers-log)| [yql](https://yql.yandex-team.ru/Operations/Yn08oAVK8BZmM_B93GBQbScEEPIaRfuVznIK3UjEXLM=)
   rthub/prestable/datacamp-offers| testing| none| none| none

#### Parser

### Исходящие
#### Событийные LB топики в Bannerland.
   Оффер будет записан в топик при изменение полей, на которые есть подписка [Market.bannerland_subscriber](https://cs.yandex-team.ru/#!Market.bannerland_subscriber,%5Emarket%2Fidx%2F,m,arcadia,,100) и [Market.bannerland_preview_subscriber](https://cs.yandex-team.ru/#!Market.bannerland_preview_subscriber,%5Emarket%2Fidx%2F,m,arcadia,,100) для preview. Так же офферы фильтруются по цвету и флагу превью.
   Name | Env | Link | Logs| Filter
   :--- | :--- | :--- | :--- | :---
   bannerland/datacamp_offers_prod| production| [link](https://lb.yandex-team.ru/logbroker/accounts/bannerland/datacamp_offers_prod)| [logs](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/bannerland_datacamp_offers_prod_log)
   bannerland/datacamp_offers_prestable| testing| [link](https://lb.yandex-team.ru/logbroker/accounts/bannerland/datacamp_offers_prestable)| [logs](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/bannerland_datacamp_offers_prestable_log)
   bannerland/blrt/preview-offers-input| production| [link](https://logbroker.yandex-team.ru/lbkx/accounts/bannerland/blrt/preview-offers-input)| [logs](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/bannerland_preview_offers_input) | флаг превью (Market.DataCamp.OfferMeta.preview) ||
   bannerland/blrt/preview-worker-test| testing| [link](https://logbroker.yandex-team.ru/lbkx/accounts/bannerland/blrt/preview-worker-test)| none | флаг превью (Market.DataCamp.OfferMeta.preview)
#### Ecom выгрузка
Sandbox задача создает выгрузку офферов из DataCamp в Export формате раз в 4 часа. Операции создания выгрузки запускаются одновременно на hahn и arnold.
**Production** выгрузка: [hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/ecom/export/offers/merged), [arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/ecom/export/offers/merged), [SB tasks](https://sandbox.yandex-team.ru/tasks?children=true&tags=ROUTINES-ECOMEXPORTMERGEDOFFERSDUMPER%2CPRODUCTION&all_tags=true&created=14_days)
**Testing** выгрузка: [hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/testing/ecom/export/offers/merged), [arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/testing/ecom/export/offers/merged), [SB tasks](https://sandbox.yandex-team.ru/tasks?children=true&tags=ROUTINES-ECOMEXPORTMERGEDOFFERSDUMPER%2CTESTING&all_tags=true&created=14_days)


## Ссылки
- [Регистрация в MBI](https://wiki.yandex-team.ru/users/moskovkin/direkt-mbi-datacamp/)
- [Топики и логфеллер](https://wiki.yandex-team.ru/market/development/indexer/arxitektura-marketnogo-indeksatora/offer-repository/integracija-s-direktom/#potokidannyx)
- [Добавление валют для директа](https://wiki.yandex-team.ru/users/fadeevsergey/novye-valjuty-v-markete/)
