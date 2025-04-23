# IDXAPI

1. [arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/api)
2. [conductor](https://c.yandex-team.ru/packages/yandex-market-idxapi "title")
3. [wiki](https://wiki.yandex-team.ru/market/development/indexer/api/)
4. log: /var/log/yandex/idxapi/idxapi.log

## production active
1. <http://active.idxapi.vs.market.yandex.net:29334/v1/smart/offer?feed_id=1069&offer_id=1>

## production
1. <http://idxapi.market.yandex.net:29334/ping>
2. <http://idxapi.market.yandex.net:29334/v1/feeds/1069/sessions/published/offers/1>

## planeshift (production)
1. <http://ps01h.market.yandex.net:29334/ping>
2. <http://ps01v.market.yandex.net:29334/ping>

## testing
1. <http://orn01ht.market.yandex.net:29334/ping>
2. <http://idxapi.tst.vs.market.yandex.net:29334/ping>

## Development
Nginx + Gunicorn + Flask + markdown

```
make run
```
## Debug
Для отладки при добавлении новых ручек достаточно собрать исполняемый файл idxapi и запустить его на дев-машине с необходимыми файлами/доступами (например, на ps01ht). После запустить на незанятом порту (дефолтный - 29334) командой

```
./idxapi -p 29335 --slow --fast
```
Ручки разнесены по времени работы на медленные и быстрые, поэтому для запуска большинства из них необходимо указать соответствующие флажки: ```--slow``` и ```--fast```.

## Depends
1. getter (currency_rates, geobase)

## API

### Версионирование

1. Основной схемой версионирования для всех без исключения API является [semver](https://h.yandex-team.ru/?http%3A%2F%2Fsemver.org%2F). Версия API состоит из трёх цифр; третья цифра изменяется при исправлении багов; вторая - при добавлении новой функциональности или объявлении старой функциональности deprecated; первая - при отказе от обратной совместимости.
2. Сервис поддерживает обращения с указанием одной, двух или трёх цифр версии:

    * idxapi/v1/endpoint
    * idxapi/v1.0/endpoint
    * idxapi/v1.0.0/endpoint

3. ```/version[?format=(json|xml)]``` - отдает текующую версию IDXAPI
4. Во всех ответах есть заголовок 'X-Market-IDXAPI', показывающий текущую версию IDXAPI

### help

Ответ поддерживается в html, json и xml (тип ответа определяется из параметра запроса ```format=[html|json|xml]```, по умолчанию html)

1. ```/help[?format=(html|json|xml)]``` - получение списка доступных ручек с помощью

Пример:
```bash
curl http://some-machine.yandex.net:29334/help?format=json | head -10
```
```json
{
    "docs": [
    {
      "help": "Ручка для проверки работоспособности инстанса idxapi",
      "methods": "HEAD,OPTIONS,GET",
      "url": "/ping"
    },
    {
      "help": "Ручка для проверки принадлежности инстанса к активному DC",
      "methods": "HEAD,OPTIONS,GET",
      "url": "/ping-is-active-dc"
    },
}
```

### ping
```/ping```

### master

ответ поддерживается в text, json и xml (тип ответа определяется из параметра запроса ```format=[json|xml|text]```, по умолчанию json)

```/v1/master```

Примеры:
```bash
curl 'http://bzz13-qtesting.haze.yandex.net:29334/v1/master'
```
```json
{
    "current_master": "stratocaster",
    "self_url": "http://bzz13-qtesting.haze.yandex.net:29334/v1/master"
}
```

### smart offer

ответ поддерживается в text, json и xml (тип ответа определяется из параметра запроса ```format=[html|json|xml|text]```, по умолчанию json)
актуальной является версия v2
ручка отдает фидовые опции доставки и ничего не знает про опции настроенные в Партнерском Интерфейсе, для получения всех опций нужно использовать ручку ```delivery```

1. ```/offer/?feed_id=<feed_id>&offer_id=<offer_id>``` - для старых потребителей редирект на умную ручку c форматом 'text' для поддержания обратной совместимости для старых потребителей

    * offer_id - **required**
    * необходим один из параметров shop_id или feed_id

2. ```/v1/smart/offer?&feed_id=<feed_id>&offer_id=<offer_id>``` - возвращает данные офера последней опубликованной полной сессии, обогащенные данным быстрой сессии (если она свежее см. **quick**)

    * offer_id - **required**
    * feed_id - **required**

Примеры:
```bash
curl 'http://bzz13-qtesting.haze.yandex.net:29334/v1/smart/offer?feed_id=1069&offer_id=1&format=text'
```
```xml
<?xml version='1.0' encoding='utf-8'?>
<feed xmlns="http://www.w3.org/2005/Atom">
    <id>1069</id>
    <title>feed 1069</title>
    <updated>2017-07-29T10:15:39Z</updated>
    <last_checked>2017-07-29T16:45:38Z</last_checked>
    <session_name>20170729_1015</session_name>
    <pickup>true</pickup>
    <entry>
        <title>testyxshop1offer1changed1</title>
        <summary>nodescrfortovar-1</summary>
        <or:price xmlns:or="http://wiki.yandex-team.ru/market/development/indexer/offersrobot/api">3.0</or:price>
        <or:shop_price xmlns:or="http://wiki.yandex-team.ru/market/development/indexer/offersrobot/api">3.0</or:shop_price>
        <or:shop_currency xmlns:or="http://wiki.yandex-team.ru/market/development/indexer/offersrobot/api">RUR</or:shop_currency>
        <or:available xmlns:or="http://wiki.yandex-team.ru/market/development/indexer/offersrobot/api">1</or:available>
        <or:onstock xmlns:or="http://wiki.yandex-team.ru/market/development/indexer/offersrobot/api">1</or:onstock>
        <link href="http://test.yandex.ru/yxshop1offer1changed1"/>
        <delivery>true</delivery>
        <local-delivery>
            <delivery-option cost="300.0" currency="RUR" day-from="0" day-to="2" order-before="24"/>
        </local-delivery>
    </entry>
</feed>
```

```bash
curl 'http://bzz13-qtesting.haze.yandex.net:29334/v1/smart/offer?feed_id=1069&offer_id=1' | head -20
```
```json
{
    "DeliveryCurrency": "RUR",
    "DeliveryOptions": [
        {
             "Cost": 300.0,
             "DaysMax": 2,
             "DaysMin": 0,
             "OrderBeforeHour": 24
        }
    ],
    "HasDelivery": true,
    "URL": "test.yandex.ru/yxshop1offer1changed1",
    "available": "1",
    "description": "nodescrfortovar-1",
    "downloaded": 1501323339,
    "feed_id": 1069,
    "last_checked": "2017-07-29T16:45:38Z",
    "offer_id": "1",
    "onstock": "1",
    "pickup": "true",
```

### feeds

Ответ поддерживается в json и xml (тип ответа определяется из параметра запроса ```format=[json|xml]```, по умолчанию json)

1. ```/v1/feeds[?format=(json|xml)]``` - получение списка метаинформации для всех фидов (тяжелая ручка, отвечает долго)
2. ```/v1/feeds/<feed_id>[?format=(json|xml)]``` - получение данных фида

Примеры:
```bash
philimonov@philimonov-desktop:~/tmp$ curl "philimonov-desktop:29777/v1/feeds"
```
```json
{
  "feeds": [
    "http://philimonov-desktop:29777/v1/feeds/1025",
    "http://philimonov-desktop:29777/v1/feeds/1036",
    "http://philimonov-desktop:29777/v1/feeds/1043",
    "http://philimonov-desktop:29777/v1/feeds/1069",
    "http://philimonov-desktop:29777/v1/feeds/1076",
    "http://philimonov-desktop:29777/v1/feeds/1086",
    "http://philimonov-desktop:29777/v1/feeds/1091",
    "http://philimonov-desktop:29777/v1/feeds/1098",
    "http://philimonov-desktop:29777/v1/feeds/1101",
    "http://philimonov-desktop:29777/v1/feeds/1112",
...
    "http://philimonov-desktop:29777/v1/feeds/449487",
    "http://philimonov-desktop:29777/v1/feeds/449489",
    "http://philimonov-desktop:29777/v1/feeds/449491",
    "http://philimonov-desktop:29777/v1/feeds/449496",
    "http://philimonov-desktop:29777/v1/feeds/449504",
    "http://philimonov-desktop:29777/v1/feeds/449506",
    "http://philimonov-desktop:29777/v1/feeds/449507",
    "http://philimonov-desktop:29777/v1/feeds/449547",
    "http://philimonov-desktop:29777/v1/feeds/449548"
  ],
  "self_url": "http://philimonov-desktop:29777/v1/feeds"
}
```

```bash
philimonov@philimonov-desktop:~/tmp$ curl "philimonov-desktop:29777/v1/feeds/1069"
```
```json
{
  "feed": 1069,
  "ff": null,
  "mbi": {
    "autobroker_enabled": "true",
    "client_id": "325076",
    "cpa": "REAL",
    "cpc": "REAL",
    "datafeed_id": "1069",
    "datasource_name": "test.yandex.ru",
    "delivery_src": "WEB",
    "delivery_vat": "4",
    "domain": "domain3.yandex.ru",
    "ff_program": "NO",
    "free": "true",
    "from_market": "true",
    "home_region": "225",
    "is_cpa_partner": "true",
    "is_discounts_enabled": "true",
    "is_enabled": "true",
    "is_mock": "true",
    "is_offline": "true",
    "is_online": "true",
    "local_delivery_cost": "1100",
    "phone": "100 495 123-45-67",
    "phone_display_options": "*",
    "prefix": "HTTP_AUTH='basic:*:marketdatabuild:********'",
    "prepay_enabled": "true",
    "prepay_requires_vat": "true",
    "price_scheme": "10;9=5;",
    "priority_region_original": "10740",
    "priority_regions": "10740",
    "promo_cpc_status": "real",
    "quality_rating": "1",
    "regions": "17;40;10030;10176;10645;10650;10658;10672;10740;10836;99064;;",
    "return_delivery_address": "Мытищи, а, дом 1, корпус 7, строение 3, 4 км, 5, пояснение длинное, 123456",
    "shipping_full_text": "В пределах Солнечный Системы за 1 джагон908 6hgh556666",
    "shop_cluster_id": "11405",
    "shop_currency": "RUR",
    "shop_delivery_currency": "RUR",
    "shop_grades_count": "220",
    "shop_id": "774",
    "shopname": "Я Тестовый шоп 4",
    "show_premium": "true",
    "subsidies": "on",
    "tariff": "CLICKS",
    "tax_system": "0",
    "url": "https://svn.yandex.ru/market/market/trunk/testshops/testdontdelete.xml",
    "urlforlog": "774.example.org",
    "use_open_stat": "true",
    "vat": "3",
    "vat_source": "WEB"
  },
  "mbi_md5": "aa0463d883405dd9eaa90e2422ebeca2",
  "self_url": "http://philimonov-desktop:29777/v1/feeds/1069",
  "status": "system",
  "ttr": 18446744073709551615
}
```

### sessions

Ответ поддерживается в json и xml (тип ответа определяется из параметра запроса ```format=[json|xml]```, по умолчанию json)
ссылки со специальными <session_id> (base, finished, published) воозвращают редирект на конкретную сессию, ассоциированную со значанием

1. ```/v1/feeds/<feed_id>/sessions[?format=(json|xml)]``` - получение списка из двух сессий (published && finished). Промежуточные сессии более нигде кроме логов не сохраняются.
    * в поле/теге "meta" возвращается десериализованный протобаф [SessionMetadata.OffersRobot](https://a.yandex-team.ru/arc/trunk/arcadia/market/proto/SessionMetadata.proto?rev=2909749#L55)

2. ```/v1/feeds/<feed_id>/sessions/finished``` - получение последней завершенной сессии для фида, если она не опубликована
3. ```/v1/feeds/<feed_id>/sessions/published``` - получение последней опубликованной сессии для фида

Примеры:
```bash
philimonov@philimonov-desktop:~/tmp$ curl "philimonov-desktop:29777/v1/sessions"
```
```json
{
  "self_url": "http://philimonov-desktop:29777/v1/sessions",
  "sessions": [
    "http://philimonov-desktop:29777/v1/feeds/1025/sessions",
    "http://philimonov-desktop:29777/v1/feeds/1036/sessions",
    "http://philimonov-desktop:29777/v1/feeds/1043/sessions",
    "http://philimonov-desktop:29777/v1/feeds/1069/sessions",
    "http://philimonov-desktop:29777/v1/feeds/1076/sessions",
    "http://philimonov-desktop:29777/v1/feeds/1086/sessions",
    "http://philimonov-desktop:29777/v1/feeds/1091/sessions",
    "http://philimonov-desktop:29777/v1/feeds/1098/sessions",
    "http://philimonov-desktop:29777/v1/feeds/1101/sessions",
...
    "http://philimonov-desktop:29777/v1/feeds/200343943/sessions",
    "http://philimonov-desktop:29777/v1/feeds/200343951/sessions",
    "http://philimonov-desktop:29777/v1/feeds/200343952/sessions",
    "http://philimonov-desktop:29777/v1/feeds/200343954/sessions",
    "http://philimonov-desktop:29777/v1/feeds/200344004/sessions",
    "http://philimonov-desktop:29777/v1/feeds/200344075/sessions",
    "http://philimonov-desktop:29777/v1/feeds/200344103/sessions",
    "http://philimonov-desktop:29777/v1/feeds/200344106/sessions",
    "http://philimonov-desktop:29777/v1/feeds/200344107/sessions",
    "http://philimonov-desktop:29777/v1/feeds/200344119/sessions"
  ]
}
```

```bash
philimonov@philimonov-desktop:~/tmp$ curl "philimonov-desktop:29777/v1/feeds/1069/sessions/published"
```
```json
{
  "feed_id": 1069,
  "meta": {
    "contents_hash": "b434QJW8pG7pCVO/gWgFaQ==",
    "deliverycalc_options_url": "https://market-mbi-test.s3.mdst.yandex.net/deliverycalculator/buckets_18710_774_dprezjrhdcsegbrpviks.pbuf.sn",
    "download_date": "2018-01-17T10:03:26",
    "download_retcode": 0,
    "download_status": "200 OK",
    "feed_url": "https://svn.yandex.ru/market/market/trunk/testshops/testdontdelete.xml",
    "feedparser": {
      "address": "",
      "agency": "",
      "bad_isbn_offers_count": 0,
      "classifier_feed_id": "4a40e6fe689d590cb091d54a4f52540a",
      "cpa_offers_count": 19,
      "cpa_real_offers_count": 19,
      "cpc_offers_count": 19,
      "cpc_real_offers_count": 19,
      "deliverycalc_bucket_ids": [
        "1243330",
        "1243331",
        "1243332",
        "1243320",
        "1243321",
        "1243322",
        "1243325",
        "1243326",
        "1243327",
        "1243328"
      ],
      "deliverycalc_generation": "18710",
      "deliverycalc_update_time_ts": "1514194202773",
      "discount_offers": 2,
      "email": "",
      "feed_id": 1069,
      "fp_version": "2018.1.22.0",
      "integrator_name": "Я Тестовый шоп 4",
      "keywords": "yxonlineshop",
      "offers_count": 19,
      "offers_hosts": "dumham.narod.ru,spbtester.narod.ru,test.yandex.ru",
      "phone_number": "",
      "platform": "",
      "region_attributes": "17 40 10030 10176 10645 10650 10658 10672 10740 10836 99064 99065 99066 99067 99068 99069 99071 99072 99073 99074 99075 99076 99077 99078 99079 99080 120848 120849 120850 121110 144203 144204 144205 144206 144207 144208 144209 144210 144211 144212",
      "regions_line": "17 40 10030 10176 10645 10650 10658 10672 10740 10836 99064 99065 99066 99067 99068 99069 99071 99072 99073 99074 99075 99076 99077 99078 99079 99080 120848 120849 120850 121110 144203 144204 144205 144206 144207 144208 144209 144210 144211 144212|Регион: 17 40 10030 10176 10645 10650 10658 10672 10740 10836 99064 99065 99066 99067 99068 99069 99071 99072 99073 99074 99075 99076 99077 99078 99079 99080 120848 120849 120850 121110 144203 144204 144205 144206 144207 144208 144209 144210 144211 144212",
      "rejected_offers_count": 0,
      "shop_comment": "",
      "shop_id": 774,
      "shop_name": "Я Тестовый шоп 4",
      "shop_priority": 1.0,
      "url": "774.example.org",
      "version": "",
      "ya_money": false,
      "yx_ds_id": 774,
      "yx_extended_ds_id": "774",
      "yx_shop_name": "Я Тестовый шоп 4"
    },
    "fp_input_hash": "addcountriesf087990d94a136076b6db333cfd00b5ecountriesb002e41b8f46204c51ea3593444aa958rates3a291c981fd1bbadb52b6994e0ae391c",
    "last_304_time": "",
    "last_modified_time": "Mon, 20 Nov 2017 15:42:36 GMT",
    "mbi_params": "shop_id\t774\nautobroker_enabled\ttrue\nclient_id\t325076\ncpa\tREAL\ncpc\tREAL\ndatafeed_id\t1069\ndatasource_name\ttest.yandex.ru\ndelivery_src\tWEB\ndelivery_vat\t4\ndomain\tdomain3.yandex.ru\nff_program\tNO\nfree\ttrue\nfrom_market\ttrue\nhome_region\t225\nis_cpa_partner\ttrue\nis_discounts_enabled\ttrue\nis_enabled\ttrue\nis_mock\ttrue\nis_offline\ttrue\nis_online\ttrue\nlocal_delivery_cost\t1100\nphone\t100 495 123-45-67\nphone_display_options\t*\nprefix\tHTTP_AUTH='basic:*:marketdatabuild:********'\nprepay_enabled\ttrue\nprepay_requires_vat\ttrue\nprice_scheme\t10;9=5;\npriority_region_original\t10740\npriority_regions\t10740\npromo_cpc_status\treal\nquality_rating\t1\nregions\t17;40;10030;10176;10645;10650;10658;10672;10740;10836;99064;99065;99066;99067;99068;99069;99071;99072;99073;99074;99075;99076;99077;99078;99079;99080;120848;120849;120850;121110;144203;144204;144205;144206;144207;144208;144209;144210;144211;144212;\nreturn_delivery_address\tМытищи, а, дом 1, корпус 7, строение 3, 4 км, 5, пояснение длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное, 123456\nshipping_full_text\tВ пределах Солнечный Системы за 1 джагон908 6hgh556666 \nshop_cluster_id\t11405\nshop_currency\tRUR\nshop_delivery_currency\tRUR\nshop_grades_count\t220\nshopname\tЯ Тестовый шоп 4\nshow_premium\ttrue\nsubsidies\ton\ntariff\tCLICKS\ntax_system\t0\nurl\thttps://svn.yandex.ru/market/market/trunk/testshops/testdontdelete.xml\nurlforlog\t774.example.org\nuse_open_stat\ttrue\nvat\t3\nvat_source\tWEB\n",
    "parse_time": "2018-01-17T10:03:40",
    "parser_retcode": 0,
    "parser_stdout": "Warning: raw data functionality is disabled, but writing to yt / local disc selected. Nothing will be written\n[2018-01-17 13:03:30] [0:0] (Message) 110 YT: transaction 93a9-4d6159-3fe0001-1ee15803 started\n[2018-01-17 13:03:30] [0:0] (Message) 110 YT: writing to hahn.yt.yandex.net\n[2018-01-17 13:03:30] [0:0] (Message) 110 YT: immediate write mode\n[2018-01-17 13:03:30] [0:0] (Message) 110 YT: creating //home/market/testing/indexer/stratocaster/or3/offers/20180117_1000\n[2018-01-17 13:03:31] [0:0] (Message) 110 YT: immediate write mode\n[2018-01-17 13:03:31] [0:0] (Message) 110 YT: creating //home/market/testing/indexer/stratocaster/or3/blue-offers/20180117_1000\n[2018-01-17 13:03:32] [0:0] (Message) 110 YT: immediate write mode\n[2018-01-17 13:03:32] [0:0] (Message) 110 YT: creating //home/market/testing/indexer/stratocaster/or3/categories/20180117_1000\n[2018-01-17 13:03:32] [0:0] (Message) 110 YT: immediate write mode\n[2018-01-17 13:03:32] [0:0] (Message) 110 YT: creating //home/market/testing/indexer/stratocaster/or3/promos/20180117_1000\n[2018-01-17 13:03:34] [0:0] (Message) 110 YT: immediate write mode\n[2018-01-17 13:03:34] [0:0] (Message) 110 YT: creating //home/market/testing/indexer/stratocaster/or3/services/20180117_1000\n[2018-01-17 13:03:35] [3:21] (Message) 162 YMLDATE= #json#{\"posColumn\":21,\"ymldate\":\"\",\"posLine\":3,\"code\":\"162\"}#/json# \n[2018-01-17 13:03:35] [14332:16] (Message) Delivery scheme: local_delivery_cost\n[2018-01-17 13:03:35] [14332:16] (Message) 110 Loading delivery options from file '/indexer/market/download/1069/20180117_1003/delivery-options.pbuf.sn'\n[2018-01-17 13:03:35] [14537:15] (Message) Audit report: #json#{\"HasBarcode\":0,\"HasClusterCategory\":0,\"HasClusterCategoryAndModel\":0,\"HasCountryOfOrigin\":0,\"HasDeliveryOptions\":0,\"HasDescription\":19,\"HasDimensions\":0,\"HasDisabledCpa\":0,\"HasGuruCategory\":0,\"HasGuruCategoryAndModel\":0,\"HasLongDescription\":0,\"HasManufacturerWarranty\":0,\"HasModel\":0,\"HasName\":19,\"HasOldPrice\":2,\"HasParam\":0,\"HasParamAge\":0,\"HasParamColor\":0,\"HasParamGender\":0,\"HasParamLine\":0,\"HasParamMaterial\":0,\"HasParamSize\":0,\"HasPicture\":19,\"HasRec\":0,\"HasSalesNotes\":19,\"HasTextParams\":0,\"HasTypePrefix\":0,\"HasVendor\":0,\"HasVendorCode\":0,\"HasWeight\":10,\"InvalidCountryOfOrigin\":0,\"InvalidDiscountOffers\":0,\"InvalidSalesNotesOffers\":0,\"StopWordSamples\":\"\",\"TotalOffers\":19,\"ValidOffers\":19}#/json# \n[2018-01-17 13:03:37] [14537:15] (Message) 110 YT: Committing transaction: 93a9-4d6159-3fe0001-1ee15803\n[2018-01-17 13:03:38] [14537:15] (Message) 110 YT: Transaction committed\n[2018-01-17 13:03:38] [14537:15] (Message) Flushed 19 offers to YT\n[2018-01-17 13:03:38] [0:0] (Message) 110 YT: (Feed stats) Saving stats to //home/market/testing/indexer/stratocaster/or3/stats\n[2018-01-17 13:03:38] [0:0] (Message) 110 YT: (Feed stats) table already exists: //home/market/testing/indexer/stratocaster/or3/stats\n[2018-01-17 13:03:38] [0:0] (Message) 110 YT: (Feed stats) Successfully logged feed stats into //home/market/testing/indexer/stratocaster/or3/stats\n[2018-01-17 13:03:38] [0:0] (Message) 161 Successfully wrote 19 valid offers of 19 total; ignored 0 duplicate offers #json#{\"totalOffers\":19,\"posColumn\":0,\"validOffers\":19,\"duplicateOffers\":0,\"posLine\":0,\"code\":\"161\"}#/json# \n[2018-01-17 13:03:38] [0:0] (Message) 260 Feed accepted. Offers total: 19, Valid offers: 19 #json#{\"validOffers\":19,\"totalOffers\":19,\"validServices\":0,\"cpcGoodOffers\":19,\"posColumn\":0,\"totalServices\":0,\"posLine\":0,\"code\":\"260\",\"offerPromos\":0,\"validCpcPromos\":0,\"validCpaPromos\":0,\"cpcRealOffers\":19}#/json# \n[2018-01-17 13:03:38] [0:0] (Message) 261 Cpa candidate offers : 19, Valid cpa offers: 19, Real cpa offers: 19, Offers with discount: 2 #json#{\"posColumn\":0,\"cpaGoodOffers\":19,\"cpaRealOffers\":19,\"posLine\":0,\"discountOffers\":2,\"cpaCandidateOffers\":19,\"code\":\"261\"}#/json# \n[2018-01-17 13:03:38] [0:0] (Message) 163 Aggregated tag stats #json#{\"vendorCode\":0,\"dimensions\":0,\"vendor\":0,\"posColumn\":0,\"posLine\":0,\"name\":100,\"picture\":100,\"sales_notes\":100,\"description\":100,\"weight\":53,\"model\":0}#/json# \n\n",
    "quick_parse_time": "2018-01-17T10:03:28",
    "session_name": "20180117_1003",
    "start_time": "2018-01-17T10:03:24"
  },
  "self_url": "http://philimonov-desktop:29777/v1/feeds/1069/sessions/published",
  "session_id": 1516183380
}
```

```bash
philimonov@philimonov-desktop:~/tmp$ curl "philimonov-desktop:29777/v1/feeds/1069/sessions/finished"
```
```json
{
  "feed_id": 1069,
  "meta": {
    "contents_hash": "b434QJW8pG7pCVO/gWgFaQ==",
    "deliverycalc_options_url": "https://market-mbi-test.s3.mdst.yandex.net/deliverycalculator/buckets_18710_774_dprezjrhdcsegbrpviks.pbuf.sn",
    "download_date": "2018-01-18T10:00:35",
    "download_retcode": 0,
    "download_status": "200 OK",
    "feed_url": "https://svn.yandex.ru/market/market/trunk/testshops/testdontdelete.xml",
    "fp_input_hash": "addcountriesf087990d94a136076b6db333cfd00b5ecountriesb002e41b8f46204c51ea3593444aa958rates3a291c981fd1bbadb52b6994e0ae391c",
    "last_304_time": "",
    "last_modified_time": "Mon, 20 Nov 2017 15:42:36 GMT",
    "mbi_params": "shop_id\t774\nautobroker_enabled\ttrue\nclient_id\t325076\ncpa\tREAL\ncpc\tREAL\ndatafeed_id\t1069\ndatasource_name\ttest.yandex.ru\ndelivery_services\t124=0;43=0;42=0;14=0;119=0;122=0;11=0;112=0;3=0;127=0;41=0;130=0;6=0;114=0;45=0;36=0;104=0;99=0;10=0;2=0;19=0;44=0;7=0;29=0;117=0;32=0;111=0;116=0;774=0;121=0;39=0;120=0;33=0;24=0;102=0;\ndelivery_src\tWEB\ndelivery_vat\t4\ndomain\tdomain3.yandex.ru\nff_program\tNO\nfree\ttrue\nfrom_market\ttrue\nhome_region\t225\nis_cpa_partner\ttrue\nis_discounts_enabled\ttrue\nis_enabled\ttrue\nis_mock\ttrue\nis_offline\ttrue\nis_online\ttrue\nlocal_delivery_cost\t1100\nphone\t100 495 123-45-67\nphone_display_options\t*\nprefix\tHTTP_AUTH='basic:*:marketdatabuild:********'\nprepay_enabled\ttrue\nprepay_requires_vat\ttrue\nprice_scheme\t10;9=5;\npriority_region_original\t10740\npriority_regions\t10740\npromo_cpc_status\treal\nquality_rating\t1\nregions\t17;40;10030;10176;10645;10650;10658;10672;10740;10836;99064;99065;99066;99067;99068;99069;99071;99072;99073;99074;99075;99076;99077;99078;99079;99080;120848;120849;120850;121110;144203;144204;144205;144206;144207;144208;144209;144210;144211;144212;\nreturn_delivery_address\tМытищи, а, дом 1, корпус 7, строение 3, 4 км, 5, пояснение длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное длинное, 123456\nshipping_full_text\tВ пределах Солнечный Системы за 1 джагон908 6hgh556666\nshop_cluster_id\t11405\nshop_currency\tRUR\nshop_delivery_currency\tRUR\nshop_grades_count\t220\nshopname\tЯ Тестовый шоп 4\nshow_premium\ttrue\nsubsidies\ton\ntariff\tCLICKS\ntax_system\t0\nurl\thttps://svn.yandex.ru/market/market/trunk/testshops/testdontdelete.xml\nurlforlog\t774.example.org\nuse_open_stat\ttrue\nvat\t3\nvat_source\tWEB\n",
    "parser_retcode": -6,
    "parser_stdout": "Warning: raw data functionality is disabled, but writing to yt / local disc selected. Nothing will be written\nStack trace:\n??+0 (0x6BAC28)\nTerminateHandler()+274 (0x6BB3F2)\nstd::terminate()+76 (0xDAD35C)\n??+0 (0xDAD911)\n??+0 (0xD83B24)\nNRecognizer::TEncodingsAndLanguages::Deserialize(char const*, char const*)+206 (0xD836EE)\nNRecognizer::TDictionaryBase::TDictionaryBase(TBlob const&)+135 (0xD814A7)\nNRecognizer::TDictionary::TDictionary(TBlob const&)+22 (0xD814F6)\nTRecognizer::TRecognizer(TString const&)+107 (0xD7773B)\nTRecognizerShell::TRecognizerShell(TString const&, unsigned long)+122 (0x9384AA)\nNFeedParser::RunMain(int, char const**)+2381 (0x2334FD)\n__libc_start_main+245 (0x7F9523B1DF45)\n\nTerminate called after throwing an instance of 10yexception\n521 yexception thrown: dict/recognize/docrec/deserialize.h:9: Premature end of data\n\n",
    "session_name": "20180118_1000",
    "start_time": "2018-01-18T10:00:32"
  },
  "self_url": "http://philimonov-desktop:29777/v1/feeds/1069/sessions/finished",
  "session_id": 1516269600
}
```

### delivery

Получение опций доставки оффера. Ответ поддерживается в формате json.

1. ```/v1/feeds/<feed_id>/sessions/<session_id>/offers/<offer_id>/delivery``` &ndash; получение "сырых" опций доставки оффера &ndash; списка бакетов и опций доставки из [Калькулятора Доставки](https://wiki.yandex-team.ru/market/projects/multiregion/deliverycalculator/) в виде десериализованных protobuf сообщений. Параметр session_id может принимать значения 'published' | 'finished'

    * бакеты: [delivery_calc.DeliveryOptionsBucket](https://a.yandex-team.ru/arc/trunk/arcadia/market/proto/delivery/delivery_calc/delivery_calc.proto#L91)
    * опции: [delivery_calc.DeliveryOptionsGroup](https://a.yandex-team.ru/arc/trunk/arcadia/market/proto/delivery/delivery_calc/delivery_calc.proto#L167).

2. ```/v1/feeds/<feed_id>/sessions/<session_id>/offers/<offer_id>/delivery?rids=<region_id>[,<region_id>,...]``` &ndash; получение дефолтных опций доставки для каждого региона, чей id передан в списке после запроса ```?rids=``` (перечисление через запятую).

    **Дефолтная опция доставки** оффера в регион &ndash; самая лучшая из потенциальных опций по критериям (по убыванию важности):

    * цена доставки (меньше &ndash; лучше),
    * максимальный срок доставки (меньше &ndash; лучше),
    * час перескока (**больше** &ndash; лучше).

    Если в ответе Калькулятора Доставки для оффера нет явной информации по запрошенному региону, доставка в него может быть разрешена &ndash; если разрешена доставка в один из **родительских** регионов из регионального дерева. В ответе ручки ```delivery``` указывается id региона, опции которого будут использованы для доставки оффера в запрошенный регион (см. примеры ответов).

    Ручка **репорта**, из которой можно получить аналогичную информацию: ```http://msh01ht.market.yandex.net:17051/yandsearch?place=offerinfo&rids=<region_id>[,<region_id>]&offerid=<ware_md5>&regional-delivery=1&show-urls=decrypted&pp=18&regset=1```.

    **Существуют отличия в ответах!** В отличие от репорта, IDXAPI:

    * **Cрок** доставки выдает в **рабочих** днях.

        Для перевода в календарные дни можно использовать ручку ```http://mi01ht.market.yandex.net:3131/calendar-converter.py?shopid=<shop_id>&days=<days>```.

Примеры:

1. ```http://localhost:29333/v1/feeds/200310239/sessions/published/offers/2/delivery```

```json
{
  "buckets": [
    {
      "carrierIds": [
        99
      ],
      "currency": "RUR",
      "deliveryOptBucketId": "2117723",
      "deliveryOptionGroupRegs": [
        {
          "deliveryOptGroupId": "2117723",
          "optionType": "NORMAL_OPTION",
          "region": 11070
        }
      ]
    },
    {
      "carrierIds": [
        99
      ],
      "currency": "RUR",
      "deliveryOptBucketId": "2117703",
      "deliveryOptionGroupRegs": [
        {
          "deliveryOptGroupId": "2117703",
          "optionType": "NORMAL_OPTION",
          "region": 959
        }
      ]
    }
  ],
  "option_groups": [
    {
      "deliveryOptionGroupId": "2117723",
      "deliveryOptions": [
        {
          "deliveryCost": "1100",
          "maxDaysCount": 11,
          "minDaysCount": 11,
          "orderBefore": 24
        }
      ]
    },
    {
      "deliveryOptionGroupId": "2117703",
      "deliveryOptions": [
        {
          "deliveryCost": "0",
          "maxDaysCount": 0,
          "minDaysCount": 0,
          "orderBefore": 24
        }
      ]
    }
  ],
  "self_url": "http://localhost:29333/v1/feeds/200310239/sessions/published/offers/2/delivery"
}
```

2. ```http://localhost:29333/v1/feeds/200310239/sessions/published/offers/2/delivery?rids=21369,213```

```json
{
  "regional_delivery_options": [
    {
      "delivery": {
        "allowed": true,
        "options": {
          "dayFrom": 4,
          "dayTo": 4,
          "order_before": 24,
          "price": {
            "currency": "RUR",
            "value": 400
          }
        },
        "region_id": 99221
      },
      "requested_region_id": 21369
    },
    {
      "delivery": {
        "allowed": false,
        "options": {},
        "region_id": null
      },
      "requested_region_id": 213
    }
  ],
  "self_url": "http://localhost:29333/v1/feeds/200310239/sessions/published/offers/2/delivery"
}
```

    В этом примере оффер

    * **Не** доставляется в регион 213;

    * Доставляется в регион 21369, при этом используются опции доставки в регион 99221. Срок доставки составляет от 4 до 4 **рабочих** дней, стоимость 400 рублей.

### refresh

Ответы в json.
Есть 2 ручки:

1. ```/v1/feeds/<feed_id>/refresh[?force=yes]``` - отправляет в офферс робот запрос на быстрый переобход фида. Опция force=yes вызывает переобход, даже если не изменился ни сам фид, ни опции из shopsdat. Ручка НЕ проверяет существование и включенность фида.
2. ```/v1/refreshes``` - получение множества всех ранее отправленных запросов для всех фидов.

### dimensions

```/v1/dimensions?shop_id=<shop_id>&warehouse_id=<warehouse_id>&offer=<feed_id>-<offer_id>&offer=<feed_id>-<offer_id>&...```

Возвращает весогабариты указанных офферов в формате JSON.
Отсутствующие или не имеющие полных весогабаритов офферы в ответ не попадают.
Если не нашлось ни одного валидного оффера, эта ручка возвращает не 404, а пустой список (```[]```).
Параметры shop_id и warehouse_id обязательны (все синие партнеры перешли в push-схему).

```bash
curl -s 'http://active.idxapi.tst.vs.market.yandex.net:29334/v1/dimensions?shop_id=43647&warehouse_id=380&offer=200374079-100126175430&offer=200374079-14137928&offer=200374079-14259609&offer=123-432' | jq
```

```json
[
  {
    "feed_id": 200374079,
    "height": 40,
    "length": 20,
    "offer_id": "100126175430",
    "weight": 3,
    "width": 30
  },
  {
    "feed_id": 200374079,
    "height": 21.001,
    "length": 10.001,
    "offer_id": "14137928",
    "weight": 1.001,
    "width": 20.001
  },
  {
    "feed_id": 200374079,
    "height": 21,
    "length": 10,
    "offer_id": "14259609",
    "weight": 2,
    "width": 20
  }
]
```

### stocks

```/v1/stocks?shop_id=<shop_id>&warehouse_id=<warehouse_id>&offer=<feed_id>-<offer_id>&offer=<feed_id>-<offer_id>&...```

Возвращает количество указанных офферов на складе поставщика в формате JSON с таймстемпом последнего обновления. Актуально для дропшип-поставщиков синего, которые передают остатки в фиде.
Отсутствующие офферы в ответ не попадают. Если не нашлось ни одного валидного оффера, эта ручка возвращает не 404, а пустой список (```[]```).
Параметры shop_id и warehouse_id обязательны (все синие партнеры перешли в push-схему).
Офферы можно передать как параметр offer в командной строке:

```bash
curl -s "http://active.idxapi.tst.vs.market.yandex.net:29334/v1/stocks?shop_id=10351558&warehouse_id=182&offer=200464948-dropSKU.7290502" | jq .
```
```json
[
  {
    "count": 190,
    "feed": 200464948,
    "offer": "dropSKU.7290502",
    "timestamp": 1579075530
  }
]
```

так и через тело запроса:
```bash
 curl --header "Content-Type: application/json" \
 --request GET \
 --data '{"offers": ["200464948-4563","200464948-8949"]}' \
 http://active.idxapi.vs.market.yandex.net:29334/v1/stocks?shop_id=10351558&warehouse_id=182
 ```

Этот вариант позволяет обойти ограничение на длину URL-a.

### check_generation
Запуск проверок индексатора над репортом. Балансер репорта выбирается через параметр balancer=[testing|stable|shadow].
Название поколения, которое мы хотим проверить передается чераз параметр name. Поколение должно быть разложено под репортом.
Параметр check_pub позволяет не ждать раскладки поколения, а сразу делать проверку.
```bash
~$ curl -vvvv "http://idxapi.vs.market.yandex.net:29334/v1/report/check_generation?balancer=shadow&name=20181221_0922&check_pub=false"
```
```
*   Trying 2a02:6b8:0:3400::4d7...
* Connected to idxapi.vs.market.yandex.net (2a02:6b8:0:3400::4d7) port 29334 (#0)
> GET /v1/report/check_generation?balancer=shadow&name=20181221_0922&check_pub=false HTTP/1.1
> Host: idxapi.vs.market.yandex.net:29334
> User-Agent: curl/7.47.0
> Accept: */*
>
< HTTP/1.1 200 OK
< Server: nginx
< Date: Fri, 21 Dec 2018 09:57:44 GMT
< Content-Type: application/json; charset=utf-8
< Transfer-Encoding: chunked
< Connection: close
< X-HOST: vla1-5933-vla-market-prod-idxap-213-8033.gencfg-c.yandex.net
< X-TIME: 16332
< X-Market-ENVTYPE: production
< X-Market-MITYPE: gibson
< X-Market-IDXAPI: 2.0.4304580
< X-Market-Req-ID: 1545386247840/e1a294a1235a5e747f89b2c9f78ac7b3
< Set-Cookie: uid=AAAfYVwcuRibfABDBJcJAg==; path=/
<
{
  "checks": {
    "check_blue_offer_price": true,
    "check_blue_promo_and_discount": true,
    "check_book_and_picture": true,
    "check_full_and_qbids_generations": true,
    "check_iphone_model_picture": true,
    "check_iphone_models": true,
    "check_mug_offer_picture": true,
    "check_mug_offers": true,
    "check_promo_and_discount": true,
    "check_red_offer_price": true,
    "check_white_offer_price": true
  },
  "status": "published"
}
* Closing connection 0
```

### check_errors_between_services
Ручка для сравнения кол-ва ошибок между 2-мя списками сервисов (или списками хостов) в одно время.
Подразумевается, что base_service - это текущий прод.
А service, это сервис, куда выкатывается новый индекс и/или репорт.
Возвращает 2 списка ошибок: 'critical' и 'warnings'.
Наличие 'critical' подразумевает остановку автоматического деплоя и начало разбирательва релиз мастером.


### check_errors_between_times
Ручка для сравнения кол-ва ошибок между 2-мя интервалами времени в наборе сервисов
Подразумевается, что base_timestamp - это более старый промежуток времени, например неделя назад.
А timestamp - текущее время.
Возвращает 2 списка ошибок: 'critical' и 'warnings'.
Наличие 'critical' подразумевает начало разбирательва релиз мастером.


### check_timings
Проверки разладки в таймингах репорта.
Алгоритм анализирует количество выбросов за контрольный промежуток времени по сравнению с накопленной историей.

Параметры запроса:
* ```color=blue|white``` - цвет репорта
* ```env=testing|prestable|production``` - какое окружение анализировать
* ```confidence=float``` - ширина доверительного интервала, мультипликатор стандартного отклонения
* ```threshold=float``` - доля выбросов среди точек проверочной выборки, достаточных для завала проверки (от 0 до 1)
* ```check_hours=int``` - размер проверочной выборки в часах
* ```train_days=int``` - размер обучающей выборки в днях
* ```only_fails=true|false``` - выводить только ошибки или всё

Пример:
```bash
$ curl 'http://localhost:29666/v1/report/check_timings?env=testing&color=white&threshold=0.0001&confidence=3&check_hours=1&train_days=3&only_fails=true'
```
```json
{"result":{"critical":{"also_viewed":0.0016181229773462784,"prime":0.0059212817833507484,"sku_search":0.0008960573476702509,"user_feed":0.005747126436781609}},"status":"done"}
```

### abo get_last_id и get_generations

Ответ поддерживается в json и xml (тип ответа определяется из параметра запроса ```format=[json|xml]```, по умолчанию json)
Для получения информации о готовых поколениях

1. ```/v1.0.0/abo/get_last_id?[released=0|1]``` - id последнего поколения. Опционально released поколение
2. ```/v1.0.0/abo/get_generations?[after=int]``` - список поколений завершенных после id в аргументе after. Без аргумента возвращает 5 последних завершенных поколений

Примеры:

```bash
curl -s http://ps03ht.market.yandex.net:8034/v1.0.0/abo/get_last_id
189472
```
```bash
curl -s http://ps03ht.market.yandex.net:8034/v1.0.0/abo/get_last_id\?released\=1
189433
```
```bash
curl -s http://ps03ht.market.yandex.net:8034/v1.0.0/abo/get_generations | jq .
[
  {
    "hostname": "mi01v",
    "id": 189472,
    "name": "20190122_1318",
    "release_date": null,
    "released": null,
    "start_date": "Tue, 22 Jan 2019 13:18:52 GMT"
  },
  {
    "hostname": "mi01h",
    "id": 189463,
    "name": "20190122_1123",
    "release_date": null,
    "released": null,
    "start_date": "Tue, 22 Jan 2019 11:23:35 GMT"
  },
  {
    "hostname": "mi01v",
    "id": 189458,
    "name": "20190122_1006",
    "release_date": null,
    "released": null,
    "start_date": "Tue, 22 Jan 2019 10:06:05 GMT"
  },
  {
    "hostname": "mi01h",
    "id": 189453,
    "name": "20190122_0913",
    "release_date": null,
    "released": null,
    "start_date": "Tue, 22 Jan 2019 09:13:21 GMT"
  },
  {
    "hostname": "mi01v",
    "id": 189447,
    "name": "20190122_0751",
    "release_date": null,
    "released": null,
    "start_date": "Tue, 22 Jan 2019 07:51:05 GMT"
  }
]
```
```bash
curl -s http://ps03ht.market.yandex.net:8034/v1.0.0/abo/get_generations\?after\=189432 | jq .
[
  {
    "hostname": "mi01v",
    "id": 189433,
    "name": "20190122_0503",
    "release_date": "Tue, 22 Jan 2019 09:17:03 GMT",
    "released": 1,
    "start_date": "Tue, 22 Jan 2019 05:03:09 GMT"
  },
  {
    "hostname": "mi01h",
    "id": 189442,
    "name": "20190122_0700",
    "release_date": null,
    "released": null,
    "start_date": "Tue, 22 Jan 2019 07:00:39 GMT"
  },
  {
    "hostname": "mi01v",
    "id": 189447,
    "name": "20190122_0751",
    "release_date": null,
    "released": null,
    "start_date": "Tue, 22 Jan 2019 07:51:05 GMT"
  },
  {
    "hostname": "mi01h",
    "id": 189453,
    "name": "20190122_0913",
    "release_date": null,
    "released": null,
    "start_date": "Tue, 22 Jan 2019 09:13:21 GMT"
  },
  {
    "hostname": "mi01v",
    "id": 189458,
    "name": "20190122_1006",
    "release_date": null,
    "released": null,
    "start_date": "Tue, 22 Jan 2019 10:06:05 GMT"
  },
  {
    "hostname": "mi01h",
    "id": 189463,
    "name": "20190122_1123",
    "release_date": null,
    "released": null,
    "start_date": "Tue, 22 Jan 2019 11:23:35 GMT"
  },
  {
    "hostname": "mi01v",
    "id": 189472,
    "name": "20190122_1318",
    "release_date": null,
    "released": null,
    "start_date": "Tue, 22 Jan 2019 13:18:52 GMT"
  }
]
```

<a name="otrace"></a>
### otrace

Возвращает ссылки, полезные для отладки индексации оффера, в формате JSON.

##### Обязательные параметры:
(любой из нижеперечисленных вариантов, главное, чтобы можно было однозначно идентифицировать оффер)

- `waremd5=<ware_md5>`
- `feed=<feed_id>&offer=<offer_id>`
- `supplier=<supplier_id | 1P>&warehouse=<warehouse_id>&shop_sku=<offer_id>`

В последнем варианте склад - опционален. Если он у поставщика не один, и не указан в запросе, считаем, что подразумевался 145 склад.

Для ID поставщика есть выделенное значение - `1P`, оно соответствует синим 1P-фидам (AXAPTA).

##### Опциональные параметры:
- `date=<YYYYMMDD>`, дата, для которой отображаются события в индексаторной трассировке (по умолчанию - сегодня)
- `rgb={green|blue}`
- `region={region_id}`, по умолчанию 213
- `rearr=<flag1=value1;flag2=value2>` - экспериментальные флаги репорта
- `params=<param1=value1&param2=value2>` - дополнительные параметры репорта
- указание флага `full` добавляет ссылки на ручки stocks/dimensions и свойства документа, относящиеся к релевантности в репорте

##### Алиасы:
- `offer = shop_sku = shop-sku`
- `waremd5 = ware_md5`
- `region = rids`
- `rearr = rearr-factors`

##### Примеры запросов:
- `/v1/otrace?feed=546765&offer=my_offer&date=20190730&full`
- `/v1/otrace?supplier=1P&warehouse=147&shop_sku=my_offer_id&rgb=blue`
- `/v1/otrace?supplier=459876&shop_sku=1243654`
- `/v1/otrace?waremd5=wa6TotstEpOtsAKXFGT0DA&rearr=market_blue_ignore_supplier_filter=1`

##### Пример выдачи:
```bash
curl -s 'http://active.idxapi.vs.market.yandex.net:29334/v1/otrace?feed=493303&offer=000048.eb9e752d-bad6-11e6-80ee-00155d000405' | jq .
```
```json
    {
        "doc_search_trace": {
             "accept_doc_filtered_reason": "OFFER_HAS_GONE",
             "document": "rFYmPfT1ONujRBagFW1MTg",
             "feed_id": "493303",
             "in_accept_doc": true,
             "in_index": true,
             "offer_id": "000048.eb9e752d-bad6-11e6-80ee-00155d000405",
             "panther_doc_rel": 0,
             "passed_accept_doc": false,
             "type": "BLUE_OFFER"
        },
        "idxapi_feed": "http://active.idxapi.vs.market.yandex.net:29334/v1/feeds/493303",
        "idxapi_published_offer": "http://active.idxapi.vs.market.yandex.net:29334/v1/feeds/493303/sessions/published/offers/000048.eb9e752d-bad6-11e6-80ee-00155d000405",
        "idxapi_smart_offer": "http://active.idxapi.vs.market.yandex.net:29334/v2/smart/offer?offer_id=000048.eb9e752d-bad6-11e6-80ee-00155d000405&feed_id=493303",
        "index_trace": "https://tsum.yandex-team.ru/trace/1561597200000/c41c7f7bca1a453315e29b8ccd421b0b",
        "offer_info": "http://rw.vs.market.yandex.net:80/yandsearch?rgb=blue&place=offerinfo&show-urls=direct&rids=213&regset=2&adult=1&pp=18&offerid=rFYmPfT1ONujRBagFW1MTg",
        "prime": "http://rw.vs.market.yandex.net:80/yandsearch?rgb=blue&place=prime&show-urls=direct&rids=213&regset=2&adult=1&pp=18&offerid=rFYmPfT1ONujRBagFW1MTg",
        "print_doc": "http://rw.vs.market.yandex.net:80/yandsearch?rgb=blue&place=print_doc&offerid=rFYmPfT1ONujRBagFW1MTg"
    }
```

<a name="msku"></a>
### msku

Возвращает все офферы данного msku и трассировку выбора оффера в байбоксе или, при указании конкретного поставщика и склада, возвращает оффер с соотвествующими параметрами

##### Обязательные параметры:

- `msku=<msku>`

##### Опциональные параметры:
- `region={region_id}`, по умолчанию 213
- `rearr=<flag1=value1;flag2=value2>` - экспериментальные флаги репорта
- `params=<param1=value1&param2=value2>` - дополнительные параметры репорта
- `cart=<offer_waremd5_1,offer_waremd5_2,offer_waremd5_3>` - waremd5 товаров, лежащих в корзине на момент выбора
- `supplier={supplier_id}` - поставщик товара для поиска конкретного оффера по msku
- `warehouse_id={warehouse_id}` - склад поставщика для поиска конкретного оффера по msku
- указание флага `full` добавляет к выводу полную трассировку buyboxDebug из ответа репорта в place=sku_offers
- указание флага `all_offers` добавляет к выводу скрытые репортом офферы msku

##### Алиасы:
- `region = rids`
- `rearr = rearr-factors`

##### Примеры запросов:
- `/v1/msku?msku=100504460732&region=213`
- `/v1/msku?msku=100504460732&full=1`
- `/v1/msku?msku=100504460732&cart=k1xNnyujE0gPGfAYKcHFJg%2CLtlsyDvEeZ2LzQ-W5dDqAA`

##### Пример выдачи:
```bash
curl -s 'http://active.idxapi.vs.market.yandex.net:29334/v1/msku?msku=100504460732&all_offers=1' | jq .
```
```json
    {
      "Все офферы с msku 100925634035": [
        {
          "FullInfoLink": "http://active.idxapi.vs.market.yandex.net:29334/v1/otrace?waremd5=cZ8Vv9hRm30CGd30PE4Ueg",
          "Status": "Выбранный оффер",
          "WareMd5": "cZ8Vv9hRm30CGd30PE4Ueg"
        },
        {
          "FullInfoLink": "http://active.idxapi.vs.market.yandex.net:29334/v1/otrace?waremd5=S62tdToh-Hvz5uvSVcNECg",
          "Status": "Оффер не выбран: Есть оффер с ценой ниже",
          "WareMd5": "S62tdToh-Hvz5uvSVcNECg"
        },
        {
          "FullInfoLink": "http://active.idxapi.vs.market.yandex.net:29334/v1/otrace?waremd5=LXFNVQESVVGdmHWDwCt_Zg",
          "Status": "Оффер скрыт на репорте и не участвовал в выборе",
          "WareMd5": "LXFNVQESVVGdmHWDwCt_Zg"
        }
      ],
      "Выбранный оффер": "cZ8Vv9hRm30CGd30PE4Ueg"
    }
```


<a name="check_supplier"></a>
### check_supplier

Быстрое получения состояния фида (поставщик + склад): индексируется ли, почему отбрасываются офферы, что попадает на выдачу и т.п.

##### Параметры
- `supplier=<int:shop_id>` - идентификатор поставщика
- `warehouse=<int:warehouse_id>`- интересующий нас склад
- `feed=<int:datafeed_id>`- id фида, если он известен
- `shop_name=<string:shop_name>`- имя поставщика, полное совпадение не требуется
- `format` - формат ответа. Если `format=json`, то будет выдан json, иначе - html.
- `only_disabled_info` - актуально только для `format=json`. Если `only_disabled_info=1`, то в выходном json будет только информация о скрытиях.

##### Пример выдачи:
```bash
curl "http://active.idxapi.vs.market.yandex.net:29334/v1/check_supplier/get?feed=703062&format=json" | jq .
```
```json
    {
      "datacamp_stats": [
        {
          "code": "45l",
          "count": 97,
          "example": {
            "SSKU": "SM180003AA"
          },
          "text": "Offer's EnrichType must be APPROVED"
        },
        {
          "code": "25g",
          "count": 26,
          "example": {
            "reason": "Offer disabled because it wasn't in complete feed"
          },
          "text": "Offer is disabled"
        },
        {
          "code": "490",
          "count": 20,
          "example": {
            "market-sku": 10381860,
            "offerId": "F14898C-2",
            "price": "6745",
            "price_limit": "6591"
          },
          "text": "The price is too high"
        },
        {
          "code": "35j",
          "count": 10,
          "example": {
            "ShopSku": 48040
          },
          "text": "No available sku sizes. Offer will be disabled"
        },
        {
          "code": "49S",
          "count": 1,
          "text": "Extra identifiers were not calculated: One of classifier_good_id,classifier_magic_id2,ware_md5 is missing (for blue: check if no msku)"
        }
      ],
      "errors": [],
      "feed_props": {
        "feed_id": 703062,
        "feed_status": "publish",
        "is_valid": true,
        "shop_id": 605725,
        "shop_name": "PRIME GROUP",
        "supplier_type": "dropship via sorting center",
        "warehouse_id": 48040
      },
      "report_stats": {
        "OFFER_DISABLED": 425,
        "OFFER_HAS_GONE": 26,
        "offers_count": 300
      },
      "stock_dimensions": {
        "in_stock_and_dimensions_specified": 313,
        "no_dimensions": 4,
        "no_stocks": 441,
        "total": 758
      }
    }
```

Если однозначно фид по указанным параметрам не получается определить, выдаёт список подходящих вариантов для выбора (актуально для html варианта).

##### Параметры запроса в репорт
- `rid=<int:region_id>`- регион, для проверки наличия доставки (по умолчанию 0 - везде)
- `rearr=<string:rearr_factors>`- экспериментальные флаги, для проверки поставщиков с нестандартными настройками
- `params=<param1=value1&param2=value2>` - дополнительные параметры репорта

##### Поиск пропавших офферов
Делает запрос в YT (через CHYT) на поиск офферов, которые были в show-логах только до пропажи, а после указанного времени - исчезли.
Таблицы большие, поэтому запрос выполняется долго.

- `lost_offers={0|1}` - поиск осуществляется только при `lost_offers=1`
- `date_lost=<yyyy-mm-dd>` - дата пропажи
- `hour_lost=<int:0-23>` - время (часы), когда офферы предположительно исчезли
- `min_lost=<00|30>` - уточнение до получасового диапазона
- `window_hours=<int:0-9>`- размер (в часах) окна времени до пропажи, офферы из которого ищем в диапазоне "пропажи"
- `window_minutes=<00|30>` - минуты (соответствуют названиям 30-минутных таблиц в show-log)
- `offer_count=<int>` - количество офферов, которое хотим получить из YT

### timeline

Ответ возвращается в виде html.

1. ```[/version]/timeline?generation=<generation>[params]``` - ручка для рисования "колбасок" со временами работы поколения

Параметры запроса

* ```generation=<string:generation_name>``` - **required** - внешний урл фида
* ```min_duration=<int:seconds>``` - минимальная продолжительность отображаемых задач
* ```host=<string:hostname>``` - хост с которого собиралась статистика (например mi01h)
* ```color=(white|blue|red|yellow)``` - цвет поколения

Для просмотра вам потребуется поддержка javascript

### override_config

Изменение значений конфигов компонентов, которые хранятся в ZooKeeper'е.

**Переход в веб-интерфейс с удобным управлением**

* [testing](http://idxapi.tst.vs.market.yandex.net:29334/v1/override_config)
* [production](http://idxapi.vs.market.yandex.net:29334/v1/override_config)
* [Master-class](https://st.yandex-team.ru/MARKETINDEXER-31265)
* [Интеграция с быстрыми конфигами](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/admin/config_daemon/README.md)

Структура запроса:

```
[/<version>]/override_config
```

##### Проставление значения конфига

Структура запроса:

`[/<version>]/override_config/set?zk-path=<zk_path>&user=<user>&reason=<reason>&section=<section>&option=<option>&value=<value>[&section=<section>&option=<option>&value=<value>&...]`

- `zk-path` - путь в ZooKeeper, по которому будет сохранен конкретный конфиг
- `user` и `reason` - поля для идентификации пользователя, который изменяет конфиг и причины изменения
- `section`, `option` и `value` - секция, параметр и новое значение конфига соответственно (можно указать произвольное число значений)

Особенности:

- Для каждого параметра нужно указывать его секцию (для корректной связи секция - параметр)
- Если по переданному пути в ZooKeeper'е нет данных, то там создается новый конфиг
- Нельзя проставлять один и тот же параметр (внутри одной секции) несколько раз
- В curl нужно передать `--request POST/PUT`

##### Удаление параметра конфига

Структура запроса:

`[/<version>]/override_config/remove?zk-path=<zk_path>&user=<user>&reason=<reason>&section=<section>&option=<option>[&section=<section>&option=<option>&...]`

- `zk-path`, `user`, `reason`, `section`, `option` - аналогично

Особенности:

- Для каждого параметра нужно указывать его секцию (для корректной связи секция - параметр)
- Нельзя удалять один и тот же параметр (внутри одной секции) несколько раз
- Если не указать параметры конфига, то конфиг (если существует) будет удален полностью по переданному пути
- В curl нужно передать `--request DELETE` и указать `--user`

##### Рекурсивное удаление параметра конфига

```[/<version>]/override_config/remove_recursive?zk-path=<zk-path>&user=<user>&reason=<reason>&section=<section>&option=<option>```

- `zk-path`, `user`, `reason`, `section`, `option` - аналогично

Особенности:

- Удаление параметра конфига по всем дочерним путям в структуре хранения конфигов ZooKeeper-а
- В curl нужно передать `--request DELETE` и указать `--user`

##### Вывод параметров конфига

Структура запроса:

`[/<version>]/override_config/show?zk-path=<zk-path>`

- `zk-path` - путь в ZooKeeper, по которому лежит конфиг

Особенности:
- Вывод в формате json

##### Вывод более глубоких путей, по которым указанный конфиг переопределяется

Структура запроса:

``` [/<version>]/override_config/check_option_override?zk-path=<zk-path>&section=<section>&option=<option>```

- `zk-path` - путь конфига в ZooKeeper
- `section` - секция параметра
- `option` - название параметра

Особенности:

- Вывод путей полных путей построчно

##### Вывод структуры хранения конфигов

Структура запроса:

```[/<version>]/override_config/show_structure?zk-path=<zk-path>```

- `zk-path` - путь конфига в ZooKeeper

Особенности:

- Древовидный вывод дочерних путей относительно пути из запроса

### admin/dukalis
Дукалис поможет расследовать судьбу ваших офферов и картинок.

- статус оффера http://idxapi.vs.market.yandex.net:29334/v1/admin/dukalis/check_offer_status/
- статус промо акции http://idxapi.vs.market.yandex.net:29334/v1/admin/dukalis/check_promo_status/
- история цены http://idxapi.vs.market.yandex.net:29334/v1/admin/dukalis/check_offer_history_price/

### admin/show
Традиционный show.py, которые показывает поколения по всем цветам. К тому же красивый :)

- <http://idxapi.vs.market.yandex.net:29334/admin/show>

### admin/bin_version
Сравнение версий бинарных файлов в разных поколениях индексации

- <http://idxapi.vs.market.yandex.net:29334/admin/bin_version>

##### Параметры
- `envtype_<id>=<str:envtype>` - envtype поколения
- `mitype_<id>=<str:mitype>`- mitype поколения
- `generation_<id>=<str:generation>`- имя поколения

`<id>` принимает значения от 0 до 9. Можно одновременно вывести до 10 поколений. 

##### Пример выдачи:
```bash
curl -sX GET 'http://idxapi.tst.vs.market.yandex.net:29334/admin/bin_version?envtype_0=testing&mitype_0=stratocaster&generation_0=20220411_1058&envtype_1=testing&mitype_1=stratocaster&generation_1=20220411_1413&format=json' | jq .
```
```json
{
  "testing-stratocaster-20220411_1058": {
    "marketindexer": "2022.2.257.0",
    "yandex-market-books": "2022.2.257.0",
    "yandex-market-models": "2022.2.257.0"
  },
  "testing-stratocaster-20220411_1413": {
    "marketindexer": "2022.2.276.0",
    "yandex-market-books": "2022.2.276.0",
    "yandex-market-models": "2022.2.276.0"
  }
}
```
