# Feedparser

- [Feedparser](#feedparser)
    - [Documentation](#documentation)
    - [Стиль тегов](#tag-style)
    - [Новые сообщения](#new-messages)
    - [1. Feedparser log messages](#1-feedparser-log-messages)
        - [1.1. Feedparser log messages format](#11-feedparser-log-messages-format)
    - [2. Feedparser error codes](#2-feedparser-error-codes)
        - [2.1. Error codes format](#21-error-codes-format)
        - [2.2. Error messages levels](#22-error-messages-levels)
        - [2.3. Error messages objects](#23-error-messages-objects)
        - [2.4. Error messages subjects](#24-error-messages-subjects)
    - [Каталог сообщений](#messages-catalog)
        - [2.4.0. Feed checker script messages](#240-feed-checker-script-messages)
        - [2.4.1. Feedparser internals related messages](#241-feedparser-internals-related-messages)
        - [2.4.2. XML related messages](#242-xml-related-messages)
        - [2.4.3. Categories related messages](#243-categories-related-messages)
        - [2.4.4. Currencies related messages](#244-currencies-related-messages)
        - [2.4.5. Offer related messages](#245-offer-related-messages)
        - [2.4.6. Feed related messages](#246-feed-related-messages)
        - [2.4.7. CSV related messages](#247-csv-related-messages)
        - [2.4.8. Promo related messages](#248-promo-related-messages)


## Documentation
1. Для магазинов
   1. [Белый YML](https://yandex.ru/support/partnermarket/export/yml.html#yml-format)
   1. [Белый CSV](https://yandex.ru/support/partnermarket/export/yml.html#text-csv)
   1. [Белый XLS](https://yandex.ru/support/partnermarket/export/basic-excel.html)
   1. [Белые акции YML](https://yandex.ru/support/partnermarket/elements/promos.html)
   1. [Синий YML](https://yandex.ru/support/marketplace/catalog/yml-elements.html)
   1. [Синий XLS](https://yandex.ru/support/marketplace/catalog/excel-fields.html)
   1. [Красный XLS](https://yandex.ru/support/marketplace-global/pricelist/formats.html#xls-csv)
   1. [Красный YML](https://yandex.ru/support/marketplace-global/pricelist/formats.html#yml-format)
   1. [Желтый YML суперчек](https://yandex.ru/support/partner-supercheck/pricelist/offline/offer.html)
1. Внутренние
   1. [Описание процесса](https://wiki.yandex-team.ru/users/ipryadkina/checkerprocedure/)
   1. [Переводы Tanker](https://tanker-beta.yandex-team.ru/project/market-partner/keyset/shared.indexer.error.codes?branch=master)
   1. [Детальные переводы, рекомендации по исправлению](https://tanker-beta.yandex-team.ru/project/market-partner/keyset/shared.indexer.error.codes.details?branch=master)
   1. [Переводы для фронта](https://wiki.yandex-team.ru/Market/frontend/Partner/docs/integration/tanker/hidden-offers/)
   1. [Фидпарсер Wiki](https://wiki.yandex-team.ru/market/development/feedparser/)

## Tag style
1. Новые теги следует согласовать с продуктологами b2b
1. Стиль новых тегов **kebab-casing**: строчными буквами через тире
1. Названия тегов без сокращений
1. Атрибуты только для метаинформации
1. Рекомендуется логические группы вкладывать в отдельные теги

## New messages
1. Перевод сообщений
   - перевод сообщений организуется менеджером продукта
   - оптимальным является предварительный заказ перевода после резервирования кода сообщения
   - сообщения без проекта управляются продуктологами: Анастасия Каячёва - контур Трафик, Василий Федосеев для синего
   - менеджерами может использоваться [форма заказа перевода](https://st.yandex-team.ru/createTicket?queue=BBM&_form=12723) в очереди BBM
   - сообщение комитится в момент разработки, без ожидания перевода, с опциональным фиче-флагом
   - перевод для неизвестных сообщений в отчетах заменяется на сообщение общего вида
   - на стороне фронта партнерки есть мониторинг сообщений без перевода
   - поддержка объяснения смысла неизвестных сообщений осуществляется менеджерами вне очереди индексатора
   - переводы используются в отчете о скрытых офферах, отчете об индексации, отчете о проверке фида (фидчекер)
1. Каталог сообщений
   - резервирование кода сообщения выполняется через комит в [readme файл репозитория](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/feeds/README.md#каталог-сообщений)
   - новые сообщения уровня 3+ должны добавляться в данный readme
   - на изменения readme файла [подписаны](https://cs.yandex-team.ru/#!market%2Fidx%2Ffeeds%2FREADME.md,notify.me,,arcadia,,5000) заинтересованные отделы
1. Уровень сообщений
   - важно соблюдать [соглашение по выбору уровня](#22-error-messages-levels)
   - уровень используется в партнерском интерфейсе для обработки результата фидчекера
   - сообщения уровня 1 и 2 партнерам не показываются и их перевод не имеет смысла
1. Контекст сообщений
   - [контекст сообщений](#23-error-messages-objects) служит для логической организации групп
   - контекст не используется формализованным способом в коде
   - большой контекст может состоять из нескольких групп
1. Параметры сообщений
   - параметры должны быть именованы
   - параметры должны добавляться через AddDetails и передаваться через json
   - параметры внутри текста сообщения смысла не имеют

## 1. Feedparser log messages

## 1.1. Feedparser log messages format

Each message produced by the feedparser (except for few fatal exception messages) is formatted as follows:
```
[YYYY-MM-DD hh:mm:ss] [line:col] (Level) [Error Code] Message
```

## 2. Feedparser error codes

### 2.1. Error codes format

A feedparser message code consists of three digits XYZ, each have a special significance:
- X - Error level
- Y - Error Object
- Z - Error Subject

The first digit denotes the error type and defines whether the message is a positive
informational report, a warning or an error.

The second digit defines the object of the error that is to say the entity the message refers to.
It can refer to such things as categories section, currencies, an offer, feed or the feedparser itself.

The last digit specifies the message subject. In other words, it describes what exactly has happened.
This digit entirely depends on the previous one.


### 2.2. Error messages levels

- 1YZ - Information - не используются в отчетах
- 2YZ - Positive/Message - не используются в отчетах
- 3YZ - **Warning** - часть оффера проигнорирована
- 4YZ - **Error** - оффер отклонен
- 5YZ - **Critical** - весь фид отклонен/критическая ошибка
- ... - **Fatal** - не смогли обработать фид из-за технических ошибок


### 2.3. Error messages objects

- X0Z - Feed checker messages
- X1Z - Feedparser internal messages
- X2Z - XML related messages
- X3Z - Messages related to feed's categories
- X4Z - Messages related to feed's currencies
- X5Z - Offer related messages 1
- X6Z - Feed related messages
- X7Z - CSV related messages
- X8Z - Promotions related messages
- X9Z - Offer related messages 2

### 2.4. Error messages subjects

Error message subject depends on the object it relates to.
The following subsections describe possible error codes and associated messages.

## Messages catalog

### 2.4.0. Feed checker script messages

- 100 _Feedchecker information and debug messages_
- 200 Successfully downloaded %s

- 501 Error reading config file: {filename}
- 502 Error occured while downloading. Aborting.
- 503 Error occured while unpacking: {errmsg}
- 504 Error patching file: {errmsg}
- 505 Error executing feedparser: {errmsg}

- 508 Archive must contain single file, %d items found
- 509 File in the archive exceeds size limit of %d Mb

- 50A Error extracting from the archive: {errmsg}
- 50A Error convert from excel to csv
- 50A Compression depth exceeded
- 50A Error

- 50B Redirects are prohibited: {response}
- 50C Malformed url: {url}
- 50D Error openning target file: {filename}
- 50E Error downloading: {errmsg}
- 50F Bad server response: {response}

### 2.4.1. Feedparser internals related messages

- 110 _Feedparser debug message_

- 511 Unknown exception occurred

### 2.4.2. XML related messages

- 421 Unknown tag in XML feed: %s

- 521 _XML parsing exception message_
- 522 Bad XML encoding! Declared XML encoding: %s, Detected XML encoding: %s
- 523 Invalid symbol occured
- 524 Invalid non printable symbol occured

### 2.4.3. Categories related messages

- 330 Category ID is too long (must be not longer than 18 symbols): <category_id>
- 331 Category ID duplicates: <category_id>
- 332 Category name is too long: "currentLength": <len>, "maxLength": <max_len>
- 333 Category has duplicates: "categoryName": <category_name>, "categoryIds": <category_ids>
- 433 Category type is not a number or unknown: %s
- 434 Forbidden category: %s
- 530 Cycle found in the category tree: <categ id> refers to <categ id>
- 531 Category name is empty: %s
- 532 Category ID is not a number: %s

### 2.4.4. Currencies related messages

- 340 Unknown currency <currency>
- 341 Invalid currency "plus" attribute value, assuming 0 by default
- 342 Duplicate currency <currency>
- 343 Wrong currency rate value
- 346 Currency outdated
- 540 Wrong currency rate value
- 541 Wrong rate value - too strong difference with cbrf rate: feed value: <rate value in the feed>, indexer value: <indexer rate value>
- 542 Unknown currency <currency>
- 543 Reference currency not found
- 544 <currency> can not be taken as a reference currency
- 545 Duplicate currency <currency>

### 2.4.5. Offer related messages

- 150 OT_SOFTWARE offer type are not supported
- 151 offer's discount rejected
- 152 offer's promo rejected
- 153 start offer parsing
- 154 offer was accepted
- 155 external service request
- 156 offer processing finished with error
- 157 offer with unknown delivery availability rejected

- 25a Cannot determine vendor and tag <vendor> not found
- 25b Cannot determine vendor and tag <vendor> not found
- 25c Model matched, but modification exists
- 25d Model name not full, model not matched
- 25e Price conflict: out of static bounds for category
- 25f Price anomaly: out of dynamic bounds
- 25g Offer is disabled
  - explicit tag in feed [<disabled>true</disabled>](https://yandex.ru/support/marketplace/catalog/additional.html?lang=ru#delete-item)
- 25h Invalid value for parameter "%s". Allowed values: ["%s", ...]
  - instead of 35g, see [MARKETINDEXER-13918](https://st.yandex-team.ru/MARKETINDEXER-13918)
- 25i MD5 not found. Can't check for duplicates
  - instead of 311, see [MARKETINDEXER-33364](https://st.yandex-team.ru/MARKETINDEXER-33364)
- 25j Offer is waiting for translation
  - instead of 314, see [MARKETINDEXER-33364](https://st.yandex-team.ru/MARKETINDEXER-33364)
- 25k Offer couldn't be send to qpipe
  - instead of 315, see [MARKETINDEXER-33364](https://st.yandex-team.ru/MARKETINDEXER-33364)
- 25l Unable to load geobase extension
- 25m No available sku sizes
  - instead of 49N, see [MARKETINDEXER-33919](https://st.yandex-team.ru/MARKETINDEXER-33919)
- 25n Hidden by MARKET_IDX
  - the most popular case - [no available sku sizes](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=7259314#L129)
- 25o Mismatched cpa/cpc scheme
  - CPA скрыт для CPC магазина или наоборот, MARKETINDEXER-37817
- 25p Ignored by unknown delivery availability
  - offers with attribute available=unknown are ignored by ADV/DBS

- 352 Invalid picture URL in the offer <picture url>
- 354 Sales notes exceed 50 characters, truncating...
- 355 Invalid barcode: %s
- 356 Duplicate offer: <offer url>
- 357 Offer pictures limit exceeded: %d
- 358 Invalid value for tag "%s": %s
- 359 Invalid offer id value: %s
- 35A Offer can't participate in CPA program : <offer url>
- 35B Invalid value for attribute "%s" of tag "%s": %s
- 35C Calculated discount value out of range
- 35D oldprice must be greater than price
- 35E oldprice is not specified, ignoring sbid (OBSOLETE)
- 35F Too long delivery-option days period
- 35G Too many delivery-option's
- 35H Delivery is false though delivery-options are specified
- 35I Too long local_delivery_days period
- 35J Duplicate entity
- 35M Too long textParams
- 35N Invalid delivery-option
- 35O Currency outdated
- 35P Wrong category for quantity specification
- 35S Invalid offer URL <offer url>
- 35T CPA offer is to be hidden
- 35U CPC offer is to be hidden due to program restrictions: <offer url>
- 35V Offer's vat doesn't match shop's taxing system
- 35W Vat must be specified only once per offer
- 35X Offer params field should end with param_separator
- 35Z Too long Shop's SKU: "currentLength": <len>, "maxLength": <max_len>
- 35a Offer has invalid quantity values. Min-quantity is not divisible by step-quantity.
- 35b Step-quantity is set automatically by Market
- 35i Offer's MARKET SKU must be published on Market
- 35j No available sku sizes
- 35k Offer's MARKET SKU doesn't exist
- 35l Too long pickup-option days period
- 35m Too many pickup-option's
- 35n Too long local-pickup-days period
- 35o Iso datetime as expiry is deprecated
- 35p Cbid is going too be deprecated, you should stop using it
- 35r Cutprice is not supported
- 35t Not supported offer type
- 35q No alcohol licence for outlet with alcohol offer
- 35u Undefined price for outlet
  - Цена должна быть указана для всего оффера либо для конкретного аутлета
- 35v Name translation can't be recognized
  - Имя не опознано как переведенный текст
- 35w English name contains non-english text
  - Английское название содержит слишком много не английского текста
- 35x Provided description contains not translated text
  - Описание не опознано как переведенный текст
- 35y Provided english description contains not translated text
  - Английское описание содержит слишком много не английского текста
- 35z Offer exceeds credit template restrictions

- 37q VAT must be 20% now
- 37r VAT must be 18% now
- 37s VAT must be 20/120% now
- 37t VAT must be 18/118% now

- 390 Offer credit templates limit exceeded, applying XXX
- 391 Unknown outlet id
  - Магазин указал в фиде аутлет, который не заведен на маркете
- 392 No delivery buckets for offer
- 393 Invalid age value
- 394 Offer and shop cpa/cpc schemes differ
- 395 Not applicable courier delivery for medicine
- 396 Offer has no required field <field>
- 397 Can not parse stocks for offer from not upload feed without yml_date
- 398 Price value differs too much from the previous value
- 399 Offer from shop with USN tax system has problem with vat
- 39A Offer has no delivery to the drop-off
  - Скорее всего, пункт приема товаров, к которому подключен партнер, не принимает данный вид товара (по карготипам)
- 39B Offer has no delivery to any region
  - У оффера нет доставки ни в один из регионов, который поддерживает Маркет (компонент NordStream)
- 39C Old price should be specified with price
- 39D The offer is not allowed for B2B sales

- 450 Invalid offer URL <offer url>
- 451 Offer price is not specified
- 452 Invalid offer price: The price aint a double number
- 453 Invalid offer price: price limit exceed
- 454 Currency is not specified for the offer
- 455 The offer refers to an unknown currency: %d
- 456 Category is not specified for the offer
- 457 The offer refers to an unknown category: %d
- 458 Duplicate offer: <offer url>
- 459 Offer title is empty
- 45A Offer declined: <offer url>
- 45B Invalid local delivery cost: <offer url>
- 45C Tag <tag> is not appropriate for offer type <type>
- 45D Invalid value for tag "%s": %s
- 45E Invalid delivery/pickup/store value because online/offline settings
- 45F Invalid category for cutpriced offer
- 45G No required tag <tag> for offer type <type>
- 45H Offers limit exceeded: %d
- 45I Invalid value for attribute "%s": %s
- 45J The bank is not found for the currency: %s
- 45K Invalid offer delivery cost: The price must be less than %s
- 45L local_delivery_cost conflicts with delivery-options - offer ignored
- 45M a conflict between new and old delivery scheme - offer ignored
- 45N Invalid delivery-option cost
- 45O Invalid delivery-option days
- 45P Invalid delivery-option order-before
- 45Q Offer seems to be alcohol
- 45R Invalid local_delivery_days
- 45S No valid picture URLs
- 45T Invalid delivery period record in delivery-option
- 45U Invalid offer category for price from=true
- 45V Offer can't participate in CPC or CPA program
- 45W No required offers's parameter <param_name>
- 45X Offer title is too long
- 45Y Offer rejected by ABO rules                // used in offers-indexer
- 45Z Unmatched offer from restricted category
  - Оффер без модели в категории с обязательными карточками
- 45a Offer belongs to a fulfilment virtual feed // used in offers-indexer
- 45b Invalid pickup period record in pickup-option
- 45c Invalid SHOP SKU
- 45d Duplicate SHOP SKU
- 45e Empty offer id
- 45f Offer is dropped due to no VAT
- 45g Offer is dropped due to shop's tax_system is not specified
- 45h Offer's vat doesn't match shop's taxing system
- 45j Offer hidden by forbidden word
- 45k Offer hidden by stop word
- 45l Offer's EnrichType must be APPROVED
- 45m Invalid delivery services format
- 45n Mapping rejected by MBOC
- 45q Original name is empty or English name is empty
- 45r Nor translated name nor english name contains text in the allowed languages
- 45s Invalid pickup-option %s
- 45t No picture: invalid picture url or waiting for download // used in offers-indexer
- 45u Offers's content does not meet the recommendations
- 45v EnglishName's length must be at least 10 for delivery service validation
- 45w Invalid model for cutpriced offer
- 45x Cutprice is forbidden
- 45y Cutprice reason is empty
- 45z Offer declined by category restrictions
  - Оффер в запрещенной категории (услуги, табак) с учетом региона

- 490 The price is too high // used in offers-indexer
  - Оффер скрыт из-за превышения предельной цены MSKU
- 491 No valid outlets in offer
  - Оффер скрыт из-за ошибок во всех аутлетах
- 492 Offer hidden as unshown
  - Оффер скрыт из-за отсутствия просмотров на маркете
- 493 Mismatch in url of the second level domain
  - CPC оффер скрыт из-за несовпадения домена второго уровня с доменом второго уровня магазина, указанного в поле domain в shops.dat
- 494 Offer seems to be non alcohol
  - У оффера выставлен флаг type=alco, однако УК считает данный товар неалкогольным
- 495 Offer's weight exceeds allowed crossdock threshold. Actual weight: <actual_weight> kg, max allowed weight: <max_allowed_weight> kg
  - Превышено максимальное допустимое значение по весу для кроссдок-оффера.
- 496 Offer's sum of dimensions exceeds allowed crossdock threshold. Actual sum of dimensions: <actual_sum_of_dimensions> cm, max allowed sum of dimensions: <max_allowed_sum_of_dimensions> cm
  - Превышено максимальное допустимое значение суммы по трём измерениям для кроссдок-оффера.
- 497 Offer hidden by ogrn
  - Оффер скрыт по ОГРН поставщика.
- 498 Offer supplier is not verified yet
  - Оффер скрыт так как ОГРН еще не проверен
- 49A 4 - Delivery and pickup flags disabled, outlets found
  - [Проверка на наличие доставок - 4](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49B 5 - Delivery and pickup flags disabled, options and outlets found
  - [Проверка на наличие доставок - 5](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49C 8 - Pickup flag disabled, no delivery options
  - [Проверка на наличие доставок - 8](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49D 1 - Delivery and pickup flags disabled, no options, no outlets
  - [Проверка на наличие доставок - 1](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49E 2 - Delivery and pickup flags disabled, options found
  - [Проверка на наличие доставок - 2](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49F 12 - Pickup flag disabled, no outlets
  - [Проверка на наличие доставок - 12](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49G 10 - Delivery flag disabled, no options
  - [Проверка на наличие доставок - 10](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49H 11 - Delivery flag disabled, options found
  - [Проверка на наличие доставок - 11](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49I 3 - Delivery and pickup flags enabled, no options, no outlets
  - [Проверка на наличие доставок - 3](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49J - Price is too high
  - Оффер скрыт из-за слишком высокой цены
- 49K 6 - Delivery and store flags disabled, no pickup
  - [Проверка на наличие доставок - 6](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49L 7 - Delivery and store flags disabled, no delivery, no pickup
  - [Проверка на наличие доставок - 7](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49M 9 - Store flag disabled, no delivery, no pickup
  - [Проверка на наличие доставок - 9](https://wiki.yandex-team.ru/users/kayacheva/newproverka/Proverka-na-nalichie-dostavok/)
- 49N No available sku sizes
- 49O Invalid category for cutprice used offer
- 49P Adult offer in non-adult category
- 49Q Crossdock offer belongs to category <prohibited_category> which is prohibited due to shoe labeling act
  - Кроссдок-оффер скрыт, так как он принадлежит категории, которая запрещена к показу согласно закону о маркировке обуви
- 49R Offer hidden by SCM. DEPRECATED MBO-27618
- 49S Extra identifiers were not calculated
- 49T Offer rejected by cis
- 49U Country of origin not filled in for DSBS offer
  - Не заполнена страна производства для DSBS оффера
- 49V Offer has not acceptable reference currency
- 49W Offer has different reference or main currencies for price and oldprice
- 49X Invalid currency for models with selling
- 49Y DSBS оffer hidden by too long delivery-option days period
  - DSBS офферы с временем доставки большим лимита не размещаются на маркете
- 49Z Offer price has unsupported currency rate
- 49a It seems there are two or more different offers with the same identifiers
- 49b Not applicable courier delivery for medicine
- 49c Not all dynamic pricing strategy values are provided
- 49d Some pictures downloaded with errors
- 49e Picture %url downloaded with error (partner site error)
- 49f Picture %url downloaded with error (technical error)
- 49g Too long Shop's SKU: "currentLength": <len>, "maxLength": <max_len>
- 49k Picture %url is invalid
- 49l Shop cannot sell jewelry
- 49m Shop cannot sell medicine
- 49n Offer's MARKET SKU must be published on Market
- 49o No MSKU in blue_enrich
- 49p Category is prohibited for self-employed
- 49q Offer price has an invalid currency for its offer type. For example TRY is valid currency only for direct offers
- 49r Dbs offer without mapping is hidden by UC category restrictions
- 49s The offer is not allowed for B2B sales
- 49t Model is not allowed for on demand
- 49u Shop cannot sell on demand
- 49v Shop cannot sell resale
- 49w Offer price in quarantine
- 49x Offer title contains an URL
- 49z No matched model card in the DSBS offer

- 550 Too many offers declined: total offers - %d, valid offers - %d, valid offers percent - %f [
      , rejected offers - %d, offers declined for bad price - %d, offers declined for bad url - %d, duplicate offers - %d
      , offers declined for bad category id - %d, offers declined for bad currency id - %d, offers declined for bad title - %d
      , offers declined for bad description - %d, offers marked HAS_GONE - %d, offers with sale-price - %d
      ]
- 551 Valid offers not found


### 2.4.6. Feed related messages

- 160 Protocol create mode. <valid offers count> valid offers of <total offers count> " total; ignored <duplicates count> duplicate offers
- 161 Successfully wrote <valid offers count> valid offers of <total offers count> total; ignored <duplicates count> duplicate offers
- 162 YMLDATE=<date>
- 163 Aggregated tag stats: {"tag1":k1,"tagN":kN}
- 164 Feed has at least one HTML offer description

- 260 Feed accepted. Offers total: <total offers count>, Valid offers: <valid offers count>
- 261 Сpa candidate offers : <total offers count>, Valid cpa offers: <valid offers count>, Real cpa offers: <real_offers_count>, Offers with discount: <discount_offers_count>
- 26a Offer available on stock, but absent in feed

- 360 Can not find shop or integrator url
- 362 Shop name length exceeds %d characters, using domain name instead: <shopname>
- 363 Invalid value for tag <cpa> in shop section
- 364 local_delivery_cost conflicts with delivery-options - delivery-options is ignored
- 365 local_delivery_cost conflicts with delivery-options - local_delivery_cost is ignored
- 366 Too many delivery-option's
- 367 Too long delivery-option days period
- 368 XML tag %s is deprecated
- 369 All offers marked HAS_GONE
- 36A Wrong order of tags with parent <parent>, tag <tagname> may be ignored
- 36B Unknown attribute name in header: %s
- 36C Too many pickup-option's
- 36D Too long pickup-option days period
- 36E Some vats in this feed was shifted
- 36F Invalid date for feed

- 460 ERROR: Shop name is empty
- 461 Shop name length exceeds 20 characters: <shopname>
- 462 Shop URL is empty
- 463 Invalid local delivery cost
- 464 Invalid value for tag "%s": %s
- 465 Shop URL is malformed: %s
- 467 Invalid delivery-option cost
- 468 Invalid delivery-option days
- 469 Invalid delivery-option order-before
- 46A Disabled CPC and CPA programs
- 46B Invalid pickup-option %s
- 46C Cashback not in range [0, 90] //deprecated
- 46D Invalid pickup period record in pickup-option
- 46E Invalid delivery period record in delivery-option

- 560 Feed declined: <exception message>


### 2.4.7. CSV related messages

- 170 INFO

- 470 Unknown attribute name in header: %s
- 471 No required attribute in header: %s
- 472 Bad row format
- 473 Bad row encoding: must be UTF-8
- 474 Wrong rows count: %d instead of %d
- 475 Dublicate attribute in header: %s

- 570 Invalid CSV header


### 2.4.8. Promo related messages

- 18v promo: offer can't be a gift to itself. Offer Id : $Id
- 18b promo: cpa offer can't have a promo. Offer Id : $Id

- 380 Missing $EntityName:$FieldName
- 381 Invalid $EntityName:$FieldName: invalid number
- 382 Invalid $EntityName:$FieldName: invalid number
- 382 Invalid $EntityName:$FieldName: not finite
- 383 Invalid $EntityName:$FieldName: invalid local date
- 384 Invalid $EntityName:$FieldName: invalid boolean
- 385 Invalid $EntityName:$FieldName: too small
- 385 Invalid $EntityName:$FieldName: too big
- 385 Invalid $EntityName:$FieldName: limit exceeded
- 386 Invalid $EntityName:$FieldName: too long
- 387 Invalid $EntityName:$FieldName: must only have alphanumerial ASCII symbols
- 388 Invalid $EntityName:$FieldName: invalid UTF-8
- 389 Invalid $EntityName:$FieldName: too much decimal places
- 38A Invalid $EntityName:$FieldName: unknown currency
- 38A Invalid $EntityName:$FieldName: unknown role
- 38A Invalid $EntityName:$FieldName: unknown promo type
- 38B Unsupported value "$value" for $EntityName:$AttributeName
- 38C Unexpected $EntityName:$AttributeName
- 38D Unknown offer-id: $id
- 38E Unknown offer-category-id: $id
- 38F Unknown service-id: $id
- 38G Duplicate $idName: $id
- 38H Duplicate service: $id
- 38I Duplicate promo id: $id
- 38J promo: offer.promo.purchase:offer-id and offer:id doesn't match
- 38L promo: required-quantity and free-quantity must both be present
- 38M promo: type incompatible with required-quantity and free-quantity params
- 38N promo: start-date must come before end-date
- 38O promo: lifetime of bonus is too short
- 38P promo: start of bonus is too far
- 38Q bundle should have from $min to $max items
- 38R promo: bundle should not contain two same models $modelId
- 38S promo: primary offer price should be bigger than half of maximal price in bundle
- 38T promo: most expensive offer in bundle should be primary
- 38V Duplicate promo $PromoId for primary product: $ProductId
- 38X promo: lowest price in bundle of $minPrice should not be less than 1% of highest price of $maxPrice
- 38Y Promos limit exceeded: $promosCount
- 38Z Services limit exceeded: $servicesCount
- 38a promo: offer too cheap for cashback //deprecated
- 38b promo: current date does not match start-date end-date range
- 38e promo: Stop word found: <word>
- 38f promo: discount not in range [5:95]
- 38g promo: $fieldName in $currency should be divisible by $divider
- 38h promo: purchase product should have one of (offer-id, category-id)
- 38i promo: $promoType purchase product should have offer-id
- 38j promo: price should be double
- 38k promo: Duplicate promo $PromoId for offer/category: $Id
- 38l promo: promo-gift must have exactly one of the attributes: offer-id, gift-id
- 38m promo: max flash-discount duration is 1 week
- 38n promo: too much promo gifts, truncated to: $num
- 38o Unknown gift-id: $id
- 38p $fieldName value should be integer, truncated to: $num
- 38q promo code discount is too large
- 38r currency of promo and offer doesn't match
- 38s promo: max required-items is $num
- 38t promo: max required-quantity is $num
- 38u promo: max free-quantity is $num
- 38v promo: no valid cashback option //deprecated
- 38w no valid promo gifts
- 38x no valid promo purchase
- 38y promo: different currencies of gifts
- 38z promo: there can be only one of 'required-items' or 'required-quantity' or 'required-sum'

- 480 promo: Unexpected parameter in promos near tag $tagName
