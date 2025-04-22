# Protocol Documentation
<a name="top"/>

## Table of Contents

- [market/proto/indexer/yt_offer.proto](#market/proto/indexer/yt_offer.proto)
    - [TOffer](#NMarketYT.TOffer)
  
  
  
  

- [Scalar Value Types](#scalar-value-types)



<a name="market/proto/indexer/yt_offer.proto"/>
<p align="right"><a href="#top">Top</a></p>

## market/proto/indexer/yt_offer.proto



<a name="NMarketYT.TOffer"/>

### TOffer



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| feed_id | [uint64](#uint64) | optional | ID фида. Значения фида берется из shops.dat (поле datafeed_id). Пример: 1069 |
| business_id | [uint64](#uint64) | optional | business ID магазина. Значение берется из shops.dat (поле business_id). |
| shop_id | [uint64](#uint64) | optional | ID магазина. Значение берется из shops.dat (поле shop_id). Пример: 206558 |
| shop_name | [string](#string) | optional | Название магазина. Значение берется из shops.dat (поле shopname). Пример: &#34;Фотосклад.ру&#34; |
| regions | [string](#string) | optional | Список неприоритетных регионов дставки. Значение берется из shops.dat (поле regions). Можно трактовать, как регионы, в который магазин чазе всего не может доставлять своими силами, а пользуется внешней доставкой. Пример: &#34;213 225&#34; |
| priority_regions | [string](#string) | optional | Приоритетный регион доставки (один регион, НЕ список!). Значение берется из shops.dat (поле priority_regions). Можно трактовать, как регион, в котором магазин может доставлять своими силами. Пример: &#34;2&#34; |
| geo_regions | [string](#string) | optional | Регионы самовывоза товара. Поле вычисляется на основе сервисов доставки магазина, значения полей pickup (интернет-магазин с возможность самовывоза) и store (магазин-салон куда можно приехать) из фида, и наличии у магазина почтоматов. Пример: &#34;213 214 215 10715 10725&#34; |
| delivery_services | [string](#string) | optional | Список грузоперевозчиков магазина. Значение берется из shops.dat (поле delivery_services). Пример: &#34;7=0;9=0;51=0;16=0;100=0;11=0;12=0;&#34; |
| shop_country | [uint64](#uint64) | optional | Страна магазина. Значение определяется по полю home_region из shops.dat, вычисляем на его основе страну. Пример: 225 |
| url | [string](#string) | optional | URL товара. Значение берется из фида (url). |
| title | [string](#string) | optional | Название товара. Значение берется из фида (title). Проверяется на наличие стоп-слов. Пример: &#34;Брюки Demix&#34; |
| description | [string](#string) | optional | Описание товара. Значение берется из фида (description). Значение проверяется на наличие стоп-слов, есть ограничение на его длину. Пример: &#34;Брюки украшены национальной символикой.&#34; |
| shop_category_id | [string](#string) | optional | Категория магазина. Значение берется из фида (categoryId). У &#34;синих&#34; офферов нет категорий. Пример: &#34;28846&#34; |
| picture_url | [string](#string) | optional | URL картинки товара. Значение берется из фида (picture). |
| downloadable | [bool](#bool) | optional | Можно ли этот товар скачать? (например, книги). Значение берется из фида (downloadable). |
| offer_id | [string](#string) | optional | ID оффера. Значение берется из фида (id). Пример: &#34;1234&#34; |
| ware_md5 | [string](#string) | optional | Уникальный хеш офера, строится на основании большинства полей в фиде. В данном поле base64 от настоящего занчения ware_md5: Base64UrlEncode(binary_ware_md5()) Пример: &#34;kOijrFDJE5Z8xj1nHxMi8g&#34; |
| model_id | [uint64](#uint64) | optional | ID групповой модели, если оффер приматчен к модели-модификации или ID обычной модели в противном случае |
| cluster_id | [uint64](#uint64) | optional | ID кластера полученный от UC |
| category_id | [uint64](#uint64) | optional | ID категории полученный от UC |
| classifier_magic_id | [string](#string) | optional | Уникальный хеш офера в котором не учитывается специфичная для магазина информация |
| price | [string](#string) | optional | Цена оффера в формате: валюта пробел цена*точность(10^7) |
| oldprice | [string](#string) | optional | Цена оффера до скидки, если unverified_oldprice &lt;= allowed_oldprice |
| allowed_oldprice | [string](#string) | optional | Максимально допустимая цена офера до скидки, рассчитаная на основании истории цен |
| unverified_oldprice | [string](#string) | optional | Цена оффера до скидки полученная от магазина |
| recommended_price | [string](#string) | optional | Цена оффера скидки, рекомендованная по price drops |
| min_price | [string](#string) | optional | Минимальная цена за последний месяц полученная после сглаживания минимумов |
| discount_percent | [int32](#int32) | optional | Процент скидки |
| flags | [uint64](#uint64) | optional | Целое число содержащее в себе бинарные флаги офера, сопоставления битов значения флагов можно найти тут: https://a.yandex-team.ru/arc/trunk/arcadia/market/library/interface/indexer_report_interface.h |
| fee | [uint64](#uint64) | optional | Комиссия за CPA заказ(1 пункт (шаг) fee равен 0.01%) |
| vendor_param_id | [uint64](#uint64) | optional | ID параметра если это вендор, получаем из MBO |
| vendor_id | [uint64](#uint64) | optional | ID вендора |
| numeric_params | [string](#string) | optional | Числовые параметры категорий, сериализованные в json |
| mbo_params | [string](#string) | optional | Параметры в формате ключ/значение полученные от MBO, сериализованные в json |
| category_color_filters | [string](#string) | optional | Гуру лайт фильтры категорий, сериализованные в json |
| regional_delivery | [string](#string) | optional | Устарело, не заполняется |
| min_quantity | [uint64](#uint64) | optional | Минимальное количество товаров в заказе |
| step_quantity | [uint64](#uint64) | optional | Минимальный шаг изменения кол-ва товаров в заказе |
| picture_urls | [string](#string) | optional | Список картинок оффрера в json формате Пример: &#34;[\&#34;https://www.kolesa-darom.ru/img/disk/big/CS29714.jpg\&#34;]&#34; |
| cpa | [int32](#int32) | optional | Участие магазина в CPA программе Возможные занчения: ENUM(ECpa, UNKNOWN=0, NO=1, SBX=2, REAL=4) |
| sales_notes | [string](#string) | optional | Заметки о товаре. Значение берется из фида (sales_notes). Значение проверяется на наличие стоп-слов, есть ограничение на его длину. Пример: &#34;Необходима предоплата&#34; |
| bid | [uint32](#uint32) | optional | Основная ставка действующая на места поисковой выдачи |
| sbid | [uint32](#uint32) | optional | Специальная ставка(для оферов на которые есть скидка) |
| cbid | [uint32](#uint32) | optional | Cтавка на клик с карточки модели |
| mbid | [uint32](#uint32) | optional | Минимальная ставка |
| barcode | [string](#string) | optional | Баркод Пример: &#34;6921499711359&#34; |
| randx | [uint32](#uint32) | optional | static_cast&lt;int&gt;(rand() / (RAND_MAX &#43; 1.0)) * offer_priority |
| outlets_data | [string](#string) | optional | BookNow point_id, region_id, in_stock |
| shop_sku | [string](#string) | optional | SKU магазина(для тех магазинов которые участвуют в программе Fulfillment) |
| pictures | [string](#string) | optional | Данные по картинкам в json формате Пример: &#34;[{\&#34;group_id\&#34;:208277,\&#34;id\&#34;:\&#34;FeFaUlI4iPnriMS3neSvbg\&#34;,\&#34;thumb_mask\&#34;:4611686018427647727,\&#34;width\&#34;:1000,\&#34;height\&#34;:1072}]&#34; |
| ff_light | [bool](#bool) | optional | deprecated всегда false - флаг участия в Fulfillment Light |
| is_blue_offer | [bool](#bool) | optional | Флаг показывает является ли оффер &#34;синим&#34;, выставляется если для магазина в shops.dat is_supplier == true |
| market_sku | [uint64](#uint64) | optional | Маркетный SKU. Значение берется из фида (market-sku). / Пример: 10479840. |
| red_status | [uint32](#uint32) | optional | Красный статус офера возможные значения: NO=1, SBX=2, REAL=4 |
| supplier_id | [uint64](#uint64) | optional | Числовой ID поставщика для синего маркета |
| supplier_name | [string](#string) | optional | Имя поставщика для синего маркета |
| supplier_type | [string](#string) | optional | Тип поставщика для синих офферов, возможные заначения &#34;1P&#34;(first party), &#34;3P&#34;(third party) |
| supplier_ogrn | [uint64](#uint64) | optional | Числовой огрн поставщика для белого маркета |
| feed_group_id | [string](#string) | optional | ID группы, произвольная строка |
| feed_group_id_hash | [string](#string) | optional | Группировочны атрибут &#43; поисковый литерал рассчитаный как hash(shop_id &#43; (model_id или cluster_id или feed_group_id)) |
| has_gone | [bool](#bool) | optional | Флаг отсутствия офера. Актуален для оферов которые сейчас не доступны, но мы ожидаем, что они могут появиться https://st.yandex-team.ru/MARKETINDEXER-11700 |
| dont_pull_up_bids | [bool](#bool) | optional | Запрет поднимать ставку до минимальной, подробнее: https://wiki.yandex-team.ru/users/intro/Ne-podnimat-moju-stavku-do-minimalnojj |
| promo_type | [uint64](#uint64) | optional | Тип промо акции (возможные зачения: https://a.yandex-team.ru/arc/trunk/arcadia/market/library/libpromo/common.h#L70) |
| api_price | [string](#string) | optional | обновленный price из api, при наличии |
| api_oldprice | [string](#string) | optional | обновленный oldprice из api, при наличии |
| api_offer_deleted | [bool](#bool) | optional | признак offer_deleted из апи |
| main_picture | [string](#string) | optional | главная картинка для офферов с текущим group_id (только для красного) |
| delivery_bucket_ids | [string](#string) | optional | Бакеты курьерской доставки (json массив) Пример: &#34;[10,20,30]&#34; |
| pickup_bucket_ids | [string](#string) | optional | Бакеты пунктов самовывоза (json массив) Пример: &#34;[10,20,30]&#34; |
| post_bucket_ids | [string](#string) | optional | Бакеты почты (json массив) Пример: &#34;[10,20,30]&#34; |
| warehouse_id | [uint32](#uint32) | optional | номер склада (для синего и красного) |
| generated_red_title | [string](#string) | optional | сгенерированное красное название из ук |
| pickup_options | [string](#string) | optional | Опции для всех пунктов самовывоза в локальном регионе |
| weight | [double](#double) | optional | вес офферв в кг |
| length | [double](#double) | optional | длина оффера в см |
| width | [double](#double) | optional | ширина оффера в см |
| height | [double](#double) | optional | высота оффера в см |
| binary_promo_md5_base64 | [string](#string) | optional | promo_id base64 encode |
| mbi_delivery_bucket_ids | [string](#string) | optional | Сквозные (MBI) бакеты курьерской доставки (json массив) |
| mbi_pickup_bucket_ids | [string](#string) | optional | Сквозные (MBI) бакеты пунктов самовывоза (json массив) |
| mbi_post_bucket_ids | [string](#string) | optional | Сквозные (MBI) бакеты почты (json массив) |
| vendor_code | [string](#string) | optional | Код производителя товара (MPN) The Manufacturer Part Number (MPN) of the product, or the product to which the offer refers. See: https://schema.org/mpn |
| vendor_string | [string](#string) | optional | Сырой vendor из фида |
| stock_store_count | [uint32](#uint32) | optional | Остатки товара на складе (актуально для синего и красного маркета) |
| delivery_options | [string](#string) | optional | Локальные опции доставки из фида, сериализованные в json |
| disabled_flags | [uint32](#uint32) | optional | Флаги скрытия оффера (биты соответствуют идентификаторам в Market::DataCamp::DataSource) |
| partner_weight | [double](#double) | optional | вес оффера в кг, полученный от партнера |
| partner_length | [double](#double) | optional | длина оффера в см, полученная от партнера |
| partner_width | [double](#double) | optional | ширина оффера в см, полученная от партнера |
| partner_height | [double](#double) | optional | высота оффера в см, полученная от партнера |
| disabled_by_dynamic | [bool](#bool) | optional | признак, что оффер будет отклонен в репорте из-за динамиков (такие оффера не участвуют в расчете mrs-статистик) |
| binary_promos_md5_base64 | [string](#string) | optional | promo_id base64 encode |
| mbi_delivery_options | [string](#string) | optional | Локальные опции доставки от СиС, сериализованные в json |
| click_n_collect_id | [string](#string) | optional | offer_id от goods |
| click_n_collect_outlets | [string](#string) | optional | outlets_id от goods |
| offers_delivery_info | [delivery_calc.mbi.OffersDeliveryInfo](#delivery_calc.mbi.OffersDeliveryInfo) | optional | Полный набор информации о досавке для оффера. Идентификаторы бакетов и модификаторов внутри - оригинальные идентификаторы от Калькулятора Доставки (не зависят от поколения индексатора). NB: Для данного поля допускаются в дальнейшем изменения формата, сохраняющие корректность YQL запросов |
| datacamp_promos | [string](#string) | optional | JSON с описанием промоакций из хранилища |
| contex_experiment_id | [string](#string) | optional | id эксперимента с коннтентом ( https://wiki.yandex-team.ru/market/report/infra/abtcontent/ ) поле выставляется только у экспериментальных (скопированных) офферов, у оригинальных офферов его нет |
| type | [int32](#int32) | optional |  |
| purchase_price | [double](#double) | optional |  |
| pricelabs_params | [string](#string) | optional |  |
| publisher | [string](#string) | optional |  |
| in_stock_count | [uint32](#uint32) | optional |  |
| model_published_on_market | [bool](#bool) | optional |  |
| market_sku_content_exp | [uint64](#uint64) | optional | если оффер экспериментальный, то в market_sku пишется id оригинального (не экспериментального) sku, а в market_sku_content_exp экспериментальный id см. https://st.yandex-team.ru/MARKETINDEXER-35078 |
| model_id_content_exp | [uint64](#uint64) | optional | если оффер экспериментальный, то в model_id_ пишется id оригинальной (не экспериментальной) модели, а в model_id_content_exp экспериментальный id см. https://st.yandex-team.ru/MARKETINDEXER-35078 |
| vendor | [string](#string) | optional | Выгрузка вендора &#34;такого же как в суперконтроллере&#34; для PriceLabs |
| offer_version | [uint64](#uint64) | optional | Глобальная версия оффера из оферного хранилища для PriceLabs |
| is_dsbs | [bool](#bool) | optional | Размещается ли оффер по программе dsbs |
| is_direct | [bool](#bool) | optional | Оффер из Direct-ТГО (https://st.yandex-team.ru/MARKETTECH-1820) |
| virtual_model_id | [uint64](#uint64) | optional | Виртуальная модель |
| is_lavka | [bool](#bool) | optional | Оффер из Яндекс.Лавки |
| is_eda | [bool](#bool) | optional | Оффер из Яндекс.Еды |
| disabled_by_dynamic_reason | [string](#string) | optional | Причина скрытия офферов динамиками |
| is_fast_sku | [bool](#bool) | optional | Признак быстрой (виртуальной) карточки |





 

 

 

 



## Scalar Value Types

| .proto Type | Notes | C++ Type | Java Type | Python Type |
| ----------- | ----- | -------- | --------- | ----------- |
| <a name="double" /> double |  | double | double | float |
| <a name="float" /> float |  | float | float | float |
| <a name="int32" /> int32 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32 | int | int |
| <a name="int64" /> int64 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64 | long | int/long |
| <a name="uint32" /> uint32 | Uses variable-length encoding. | uint32 | int | int/long |
| <a name="uint64" /> uint64 | Uses variable-length encoding. | uint64 | long | int/long |
| <a name="sint32" /> sint32 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. | int32 | int | int |
| <a name="sint64" /> sint64 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. | int64 | long | int/long |
| <a name="fixed32" /> fixed32 | Always four bytes. More efficient than uint32 if values are often greater than 2^28. | uint32 | int | int |
| <a name="fixed64" /> fixed64 | Always eight bytes. More efficient than uint64 if values are often greater than 2^56. | uint64 | long | int/long |
| <a name="sfixed32" /> sfixed32 | Always four bytes. | int32 | int | int |
| <a name="sfixed64" /> sfixed64 | Always eight bytes. | int64 | long | int/long |
| <a name="bool" /> bool |  | bool | boolean | boolean |
| <a name="string" /> string | A string must always contain UTF-8 encoded or 7-bit ASCII text. | string | String | str/unicode |
| <a name="bytes" /> bytes | May contain any arbitrary sequence of bytes. | string | ByteString | str |

