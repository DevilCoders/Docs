# SaaS в офферном хранилище
SaaS — это общеяндексовый сервис для полнотекстового поиска по коллекции документов. Подробнее про сервис можно почитать на [вики](https://wiki.yandex-team.ru/jandekspoisk/saas/) и не стоит его путать с saashub. В офферном хранилище SaaS используется для поиска офферов партнера в партнерском интерфейсе, еще одним потребителем является MBI.

## Отправка документов в SaaS
Конвертацией офферов в поисковые документы и отправка происходит в контроллерах. Конвертация происходит в процессоре [saas_docs](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/saas_docs), а отправка в [saas_api_sender](https://a.yandex-team.ru/arc/trunk/arcadia/saas/common_proxy/processors/saas_api_sender?rev=r7782942) через топики в logbroker.

Регулярная задача в рутинах создает список оферов, для которых состояние документа в SaaS неактуально, для переотправки через сканер - [saas_diff_builder](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/tasks/saas_diff_builder).

### Идентификаторы документов
Все документы в SaaS разделяются на множества по `kps`, в случае хранилища идентификатором `kps` является `business_id` оффера. У каждого документа есть свой уникальный составной идентификатор, для офферов это `s/{business_id}/{offer_id}`, отсюда можно заметить, что в одном документе содержатся атрибуты базового и сервисных офферов. В название некоторых атрибутов из сервисных офферов добавляется суффикс с идентификатором магазина/сервиса.

## Атрибуты/литералы
Существует три вида атрибутов: поисковые, группировочные и проперти.

### Поисковые атрибуты
Поисковые атрибуты используются для фильтрации документов.

#### Именование поисковых литералов
Поисковые литералы должны начинаться со специального префикса в зависимости от типа ([документация](https://doc.yandex-team.ru/Search/saas/saas-overview/concepts/json-doc.html))

Если лень читать документацию
- целочисленный поисковый литерал должен начинаться с `i_`
- строковый поисковый литерал с `s_`
- название зоны должно начинаться с `z_`. Зоны являются своего рода неймспейсами внутри документа. В нашем случае зона используется для полнотекстового поиска по строковым полям.

#### Список поисковых литералов
- `s_doc_type` - тип документа (на текущий момент поддерживается только `offer`)
- `s_offer_id` - идентификатор оффера
- `s_shop_id` - идентификаторы магазинов/сервисов, в которых создан оффер
- `i_publish_by_partner` - идентификаторы магазинов/сервисов, в которых оффер размещается
- `s_vendor` - производитель либо бренд товара, значение из [offer.content.partner.original.vendor](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L287)
- `s_leaf_category_id` - идентификатор магазинной категории, к которой привязан оффер, значение из [offer.content.partner.original.category.id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L408)
- `s_category_id` - идентификаторы магазинных категорий, включая родительские, в которых находится оффер, значение из [offer.content.partner.original.category.path_category_ids](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L408)
- `s_market_category_id` - идентификатор маркетной категории, к которой привязан оффер, значение из [offer.content.binding.approved.market_category_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMapping.proto?blame=true&rev=r7768214#L63)
- `s_variant_id` - идентификатор варианта, привязка маркетной модели от ультраконтроллера, значение из [offer.content.binding.uc_mapping.market_model_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMapping.proto?blame=true&rev=r7672382#L66)
- `i_group_id` - идентификатор группы офферов партнера, значение из [offer.content.partner.original.group_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L314)
- `s_certificate` - идентификаторы сопроводительных документов, значение из [offer.content.master_data.certificates](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r7837080#L884)
- `i_result_status_{shop_id}` - интегральный статус оффера в конкретном мазагине/сервисе, учитывает скрытия от партнера, от маркета, ABO, MBOC, MDM, MBI, PRICELABS, а также статус индексации, значение из [offer.status.result](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=65a3216d356f5db6ce345379f71f1a235082d6df#L58)
- `i_dynamic_pricing_type_{shop_id}` - тип динамического ценообразования, значение из [offer.price.dynamic_price.type](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferPrice.proto?rev=8511473#L131)
- `i_united_catalog` [_Legacy_] - значение использовалось во время миграции офферов в единый каталог [offer.status.united_catalog](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r8102129#L162). На данный момент всегда заполняется = true. Планируется к удалению.
- `i_content_cpa_status` - CPA статус оффера, полученный от контент системы, значение из [offer.content.status.content_system_status.cpa_state](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/ContentStatus.proto?rev=r7766166#L34)
- `i_integral_content_status` - интегральный статус карточки товара, значение из [offer.content.status.result.card_status](hhttps://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/ContentStatus.proto?rev=r7916965#L163)
- `i_allow_model_create_update` - редактируемость PSKU, значение из [offer.content.status.content_system_staus.allow_model_create_update](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/ContentStatus.proto?rev=r7766166#L40)
- `i_supply_plan_{shop_id}` - статус плана по поставкам в конкретном магазине/сервисе, значение из [offer.content.partner.original_terms.supply_plan](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r7837080#L503)
- `i_mapping_change_ts` - момент изменения маппинга карточки согласно данным MBOC, значение из [offer.content.binding.approved.msku_change_ts_from_mboc](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMapping.proto?rev=r9154890#L126)
- `i_current_mapping_state` - статус маппинга карточки, значение вычислимо: зависит от равенства [content.binding.approved.market_sku_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMapping.proto?rev=r9201160#L120) и [content.binding.partner_mapping_moderation.partner_decision.market_sku_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMapping.proto?rev=r9201160#L178)
- `i_creation_hour_ts` - момент создания оффера, значение из [offer.meta.ts_first_added](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r9339038#L37) либо [offer.meta.ts_created] https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r9339038#L31), округленное до часа
- `i_verdict` - множественный, хеш вердикта из базовой части, соответствует [verdicts](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/routines/verdicts/recent)
- `i_verdict_{shop_id}` - множественный, хеш вердикта из соответствующей сервисной части и акт.сервисных частей, соответствует [verdicts](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/routines/verdicts/recent)
- `s_market_sku_id` - привязка к маркетной карточке, значение из [offer.content.binding.approved.market_sku_id](https://a.yandex-team.ru/svn/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMapping.proto?rev=r9654892#L150)

#### Список зон для полнотекстового поиска
- `z_offer_id` - идентификатор оффера
- `z_name` - полное название оффера, значение из [offer.content.partner.original.name](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L268)
- `z_vendor` - производитель либо бренд товара, значение из [offer.content.partner.original.vendor](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L287)

### Группировочные атрибуты
Группировочные атрибуты используются для группировки выдачи по значению атрибута или сортировки. Также группировочные атрибуты используются для подсчета статистик(фасетов). Специальных правил нейминга группировочных атрибутов нет. Строковым группировочным атрибутам лучше давать уникальные названия.

#### Список группировочных атрибутов
- `doc_type` - тип документа (на текущий момент поддерживается только `offer`)
- `vendor` - производитель либо бренд товара, значение из [offer.content.partner.original.vendor](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L287)
- `leaf_category_id` - идентификатор магазинной категории, к которой привязан оффер, значение из [offer.content.partner.original.category.id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L408)
- `category_id` - идентификаторы магазинных категорий, в которых находится оффер, значение из [offer.content.partner.original.category.path_category_ids](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L408)
- `group_id` - идентификатор группы офферов партнера, значение из [offer.content.partner.original.group_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L314)
- `mboc_consistency` - консистентность офферов с точки зрения MBOC, значение из [offer.status.consistency.mboc_consistency](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r7830078#L204)
- `allow_model_create_update` - редактируемость PSKU, значение из [offer.content.status.content_system_staus.allow_model_create_update](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/ContentStatus.proto?rev=r7766166#L40)
- `market_category_id` - идентификатор маркетной категории, к которой привязан оффер, значение из [offer.content.binding.approved.market_category_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMapping.proto?blame=true&rev=r7768214#L63)
- `i_result_status` - интегральный статус оффера во всем бизнесе. `i_result_status=1` если есть хотя бы один магазин, где у оффера статус `PUBLISHED`, иначе `i_result_status=0`
- `cargo_type` - список карготипов оффера, значения из [offer.content.master_data.cargo_type](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r8634816#L1193)
- `market_vendor_id` - производитель либо бренд товара, значение из [offer.content.market.vendor_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r8461619#L203)
- `creation_ts_sort_relevance` - атрибут для сортировки по дате создания: модифицированный таймстемп создания базовой части, дополненный хэшем, значение таймстемпа - из [offer.meta.ts_first_added](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r9147884#L35) если есть, иначе из [offer.meta.ts_created](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r9147884#L31).
- `offer_id_ga` - идентификатор оффера
- `name_ga` - полное название оффера, значение из [offer.content.partner.original.name](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L268)
- `card_rating` - уровень заполненности параметров офера по текущему состоянию в мбо [offer.content.partner.market_specific_content.rating.current_rating](https://a.yandex-team.ru/arcadia/market/idx/datacamp/proto/offer/OfferMarketSpecificContent.proto?rev=r9562145#L35)
- `partner_stock_{shop_id}` - значение партнерского стока
- `price_{shop_id}` - значение цены
- `market_sku_id` - привязка к маркетной карточке, значение из [offer.content.binding.approved.market_sku_id](https://a.yandex-team.ru/svn/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMapping.proto?rev=r9654892#L150)

### Проперти документа
Проперти документа — это снипеты, которые возвращаются в выдаче, при поиске и фильтрации они никак не используются. В большинстве случаев проперти были добавлены для дебажных целей.
- `offer_id` - идентификатор оффера
- `doc_type` - тип документа (на текущий момент поддерживается только `offer`)
- `vendor` - производитель либо бренд товара, значение из [offer.content.partner.original.vendor](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L287)
- `leaf_category_id` - идентификатор магазинной категории, к которой привязан оффер, значение из [offer.content.partner.original.category.id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L408)
- `category_id` - идентификаторы магазинных категорий, в которых находится оффер, значение из [offer.content.partner.original.category.path_category_ids](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L408)
- `variant_id` - идентификатор варианта, привязка маркетной модели от ультраконтроллера, значение из [offer.content.binding.uc_mapping.market_model_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMapping.proto?blame=true&rev=r7672382#L66)
- `group_id` - идентификатор группы офферов партнера, значение из [offer.content.partner.original.group_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L314)
- `mboc_consistency` - консистентность офферов с точки зрения MBOC, значение из [offer.status.consistency.mboc_consistency](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r7830078#L204)
- `market_category_id` - идентификатор маркетной категории, к которой привязан оффер, значение из [offer.content.binding.approved.market_category_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMapping.proto?blame=true&rev=r7768214#L63)
- `publish_by_partner` - идентификаторы магазинов/сервисов, в которых оффер размещается
- `cargo_type` - список карготипов оффера, значения из [offer.content.master_data.cargo_type](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r8634816#L1193)
- `market_vendor_id` - производитель либо бренд товара, значение из [offer.content.market.vendor_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r8461619#L203)
- `name` - полное название оффера, значение из [offer.content.partner.original.name](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L268)

## Поисковые запросы
Ручка поиска и язык поисковых запросов достаточно обширен, подробнее про них можно прочитать в следующих записях [Отправка запросов](https://doc.yandex-team.ru/Search/saas/saas-overview/concepts/searching.html), [Язык поисковых запросов](https://doc.yandex-team.ru/Search/saas/saas-overview/concepts/q-lang.html), [Операторы поиска](https://yandex.ru/support/search/query-language/search-context.html). Здесь же будут примеры некоторых запросов в образовательных целях и некоторые особенности запросов для документов хранилища.

### Балансеры
* Тестинг `http://prestable-market-idx.saas.yandex.net:80`, TVM_ID=2023694
* Production `http://stable-market-idx.saas.yandex.net:80/`, TVM_ID=2023672
* Название сервиса `market_datacamp` в обоих средах

{% note warning %}
Для походов в production среде потребуется TVM авторизация, можно запросить у @isabirzyanov.
{% endnote %}

### Оффера, конкретного shop_id
- shop_id = 10447289
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp?ms=proto&hr=da&debug=da&kps=10441395&text=s_shop_id%3A%2210447289%22
```

### Оффера, НЕ опубликованные в shop_id
Оператор ```A ~~ B``` вычитает документы, подходящие под запрос B, из A. ```text=s_doc_type:offer ~~ i_publish_by_partner:{shop_id}```
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp?hr=da&ms=proto&kps=10441395&numdoc=5&text=s_doc_type%3A%22offer%22%20%7E%7E%20i_publish_by_partner%3A1
```

### Оффер конкретного shop_id по offer_id
- shop_id = 10447289
- offer_id = "15"
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp?ms=proto&hr=da&debug=da&kps=10441395&text=s_shop_id%3A%2210447289%22%20s_offer_id%3A%2215%22
```

### Детерменированный порядок выдачи
Выдача по умолчанию сортируется по релевантности, и при равенстве релевантности порядок неопределен. Таким образом оффер может скакать между разными страницами. Чтобы этого избежать надо в запрос добавить ``relev=calc=sort_hash:fnvhash_f32(zdocid_i64())``. Подробное описание в тикете [SAASSUP-2804](https://st.yandex-team.ru/SAASSUP-2804).
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp?ms=proto&hr=da&debug=da&kps=10441395&relev=calc%3Dsort_hash%3Afnvhash_f32%28zdocid_i64%28%29%29&text=s_shop_id%3A%2210447289%22
```

### Все возможные значения группировочного атрибута
- Название группировочных атрибутов передаются в gafacets, имена разделяются запятыми
- При запросе значения аттрибута X добавляется qi=facet_X, см. пример
- Результаты записывается в ```SearcherProp[i]``` в формате ```<prop_value1>:<cnt1>;<prop_value2>:<cnt2>```
- [Wiki статистика по документам](https://wiki.yandex-team.ru/jandekspoisk/SaaS/stat/)
- [Формирование выдачи](https://doc.yandex-team.ru/Search/saas/saas-overview/concepts/how-search-works.html?lang=ru)
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp?ms=proto&hr=da&debug=da&kps=10441395&text=s_doc_type%3Aoffer&gafacets=vendor%2Ccategory_id&qi=facet_vendor&qi=facet_category_id&how=docid&haha=da&numdoc=1
```

### Suggest
- Саджест настроен по следующим полям: ``name, offer_id``.
- [Подробнее про типы саджестов в SaaS](https://wiki.yandex-team.ru/jandekspoisk/saas/suggest/)

Параметры запроса:
- sgkps - business_id
- relev=formula=suggest_pln формула релевантности (сейчас в сервисе только одна формула suggest_pln)
- skip-wizard=1&component=Suggest обязательные параметры для саджеста
- text по какому тексту саджестить
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp?ms=proto&hr=da&debug=da&sgkps=10441395&skip-wizard=1&component=Suggest&relev=formula=suggest_pln&text=iphone
```

## Добавление нового атрибута
1. Разметить подписку на прото поле, подписчик `saas_subscriber`
2. Добавить конвертацию поля в атрибут в [document.cpp](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/saas_docs/document.cpp)
3. Проверить заполнение поля в [document_ut.cpp](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/saas_docs/ut/document_ut.cpp)
4. Добавить описание атрибута в эту [документацию](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/docs/other/saas.md)
5. После релиза все документы переиндексируются в течение недели

## Дополнительные ссылки
- [SaaS в индексаторе](https://wiki.yandex-team.ru/market/development/indexer/market-saas/)
- [SaaS FAQ](https://wiki.yandex-team.ru/jandekspoisk/saas/saas-faq/)
- [Утилита saas_client](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/saas_client/README.md?rev=7096384&blame=true)
- [Обновление всего стейта SaaS с помощью ферримана](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/build_ferryman_table)

## Графики и мониторинги
Основной дашборд сервиса от команды SaaS [stable](https://saas-mon.n.yandex-team.ru/monitor/?ctype=stable_market_idx&service=market_datacamp&kind=backend&dc=&allserv=) и [testing](https://saas-mon.n.yandex-team.ru/monitor/?ctype=prestable_market_idx&service=market_datacamp&kind=backend&dc=&allserv=)

## Где мой документ?
Шаблон запроса для поиска документа в стейте SaaS и логфеллере: [https://yql.yandex-team.ru/Operations/YhkeRFZ1O89BppGhQBFTkNaXXNxgPDn9NjbCjd1NcvM=](https://yql.yandex-team.ru/Operations/YhkeRFZ1O89BppGhQBFTkNaXXNxgPDn9NjbCjd1NcvM=)

### Документы в стейте SaaS
Можно залезть во внутренние таблицы SaaS и посмотреть там свои документы, для этого надо знать [url документа](#identifikatory-dokumentov): [таблица тестинга](https://yt.yandex-team.ru/arnold/navigation?path=//home/saas/ferryman-prestable-market-idx/market_datacamp/workspace/state/main), [таблица прода](https://yt.yandex-team.ru/arnold/navigation?path=//home/saas/ferryman-stable/market_datacamp/workspace/state/main).

Пример запроса: [https://yql.yandex-team.ru/Operations/YhjT1K5OD3u9Rd8vmFAnk0jqn_sJjHHfyY2Flt_fDs4=](https://yql.yandex-team.ru/Operations/YhjT1K5OD3u9Rd8vmFAnk0jqn_sJjHHfyY2Flt_fDs4=)

### Logfeller
У SaaS настроен пятиминутный логфеллер по отправленным документам: [таблицы тестинга](https://yt.yandex-team.ru/arnold/navigation?path=//home/saas-lb-delivery/lbkx/saas/services/market_datacamp/prestable_market_idx/topics), [таблицы прода](https://yt.yandex-team.ru/arnold/navigation?path=//home/saas-lb-delivery/logbroker/saas/services/market_datacamp/stable/topics). Стоит учитывать, что все топики шардированы по хешу от урла.

Пример поиска отправки конкретного оффера с идентификаторами `business_id=918444 offer_id="25066v-52"`
1. Определяем шард
   * Быстрый вариант с расчетом city_hash: [yql](https://yql.yandex-team.ru/Operations/YhkpepfFt5WQl4BaKsKsFrOpn6wLeaEDTv2K2HZmMtg=)
   * Медленный вариант с поиском документа в [стейте SaaS](#documenty-v-steyte-saas). В поле `ShardIndex` лежит номер нашего шарда.
2. Выбираем папку с названием, содержащим диапазон, в который попадает найденный шард
3. Ищем по пятиминутным табличкам: [запрос](https://yql.yandex-team.ru/Operations/YhjXdAVK8CgkLcErBECHEvSvOHbtjWxReHAf6in2Ogs=). Красота в запросе получена так:
    * собрать arcadia/contrib/tools/protoc/bin/protoc
    * запустить `ya yql proto_field`, пример: `ya yql proto_field -m TDocument -p saas/protos/rtyserver.proto -a /home/thesonsa/arc/arcadia --protoc /home/thesonsa/arc/arcadia/contrib/tools/protoc/bin/protoc -r ignore`
    * использовать в запросе meta из результата ([пример результата](https://paste.yandex-team.ru/7535084/text))
4. Видим отправку: 25 февраля 2022 г., 6:50:00 MSK (т.к. в табличке `1645761000-300`), отправлен документ: [документ](https://paste.yandex-team.ru/7533456/text).
