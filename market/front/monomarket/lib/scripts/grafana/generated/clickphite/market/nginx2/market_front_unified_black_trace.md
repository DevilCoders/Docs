# market/nginx2/market_front_unified_black_trace
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `market_front_trace`

## Splits

```json
{
    "target_module": "coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE')",
    "request_method": "coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD')",
    "error": "replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_')",
    "code": "concat(substring(toString(http_code),1,1),'xx')",
    "page": "replaceAll(page_id, ':', '_')",
    "dc": "multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' )",
    "host": "host",
    "requester": "multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\\\)|MSRBOT \\\\(http://research\\\\.microsoft\\\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\\\.com|Refer\\\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' )",
    "region": "replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_')"
}
```

## Filters

```json
[
    "environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_black_desktop'",
    "environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != ''",
    "environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != ''"
]
```

## Resulting metrics

  * [`market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#c0aba132781c404f258550b1b7458be4)
  * [`market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps`](#6de1d1daa932e9d78fa50c2106434cc3)
  * [`market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#b2ee25a4162345c7b63d821d4ba5aa40)
  * [`market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#4a7abf31bfecfc418689b12947ca6cd9)
  * [`market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps`](#e12b2149fb75315839afa5c8e759ea43)
  * [`market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#4a2322e3c82719a8835cd3b29d271770)
  * [`market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps`](#a2060b36e76f7638c5bc634ba7e5c9e5)
  * [`market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#e671d7d63003cebce4f3aea905225071)
  * [`market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#3699ae683f599c5bcc1f06adf2ca881f)
  * [`market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps`](#a15170970cb1bd4059f01650cf884944)
  * [`market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#7f9971d85b88bfce739290ed62ba9516)
  * [`market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#6fc71a57527066cbcb2c39056bd235ff)
  * [`market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps`](#79609137a100d8b15e3ad53efa9a80d8)
  * [`market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#8fabeadcba345be91d760f017a637593)
  * [`market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps`](#e742751e8597005adff3d3d804e9e988)
  * [`market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#f58055bb8a6de5ea85da8bb15622cd0d)
  * [`market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#46b0b40b2eebb52ac7eaa33557893a95)
  * [`market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps`](#b29f8e17da377677ed5de95f81ff8cf0)
  * [`market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#d8ccb102f6bc221b4d9f24cb38e73864)
  * [`market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#69d801cc90e14855862a4f2be432527d)
  * [`market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps`](#85ba5631727ffc41965edc3c8ba9e6c1)
  * [`market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#ab996aca2fd385f6e0ad3ad709db6af2)
  * [`market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps`](#ae2b070237006a424f3d3eb01f025f18)
  * [`market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#9a98a107bea4c4d0b2751ff43bb26534)
  * [`market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#b22e06248c46141a0d22142f867692d6)
  * [`market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps`](#6993156f45497c51999cca71f93b1705)
  * [`market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#8329fb25c4a9fa01317da277b7ee33a0)
  * [`market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#ac2e3841d37be7c4e2a40f7b8f6dce57)
  * [`market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps`](#4cab1dc706b33259fda63bebfc513bd0)
  * [`market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#9b4478a5f16283b0e305a062a403c6e3)
  * [`market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps`](#b661e5c78ed72d38b1bde43638de1d4c)
  * [`market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#dfef6ddf234cfb246e218c345bc0c489)
  * [`market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#6aaed0ffe7d1f128cc334b7eb9cbd961)
  * [`market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps`](#597cb0cc33f4aa6285b3f88ff97faabb)
  * [`market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#b0b5095920751754fb7ea95fffbb4802)
  * [`market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#3dd2eae6e64917c48143f033ede4ef40)
  * [`market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps`](#2772b8324594f3f6cced978c8d6fb5f4)
  * [`market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#b07ba0a5d319f49924fe20f6facb6c3b)
  * [`market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps`](#b3a06c1f7aad6babba0d69174bc4d0c5)
  * [`market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#1f8ae1138fbacef6ce8b8b0d8c5b7ee6)
  * [`market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#f11195bd6ff5ba9b2f66c0c066d3d678)
  * [`market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps`](#aadf50312fc554cc8ea5b66455390773)
  * [`market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#ca2f48f3c68764ec162f0cc193869619)
  * [`market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#9422843d25939d85873b908a110061af)
  * [`market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps`](#0eec51673452989b93e0ed95ef2fed9d)
  * [`market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#8f22e0a6ff228eb52ab52374ec302190)
  * [`market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps`](#a5c761456970a1a71839333db76112e2)
  * [`market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#875f46a571540aa847bb8c4fe787dcf3)

## Metrics

#### <a id='a5c761456970a1a71839333db76112e2'></a>market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='875f46a571540aa847bb8c4fe787dcf3'></a>market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method,
        error
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a2060b36e76f7638c5bc634ba7e5c9e5'></a>market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e671d7d63003cebce4f3aea905225071'></a>market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        dc,
        target_module,
        request_method,
        error
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e742751e8597005adff3d3d804e9e988'></a>market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f58055bb8a6de5ea85da8bb15622cd0d'></a>market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        host,
        target_module,
        request_method,
        error
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b3a06c1f7aad6babba0d69174bc4d0c5'></a>market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1f8ae1138fbacef6ce8b8b0d8c5b7ee6'></a>market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        requester,
        target_module,
        request_method,
        error
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0eec51673452989b93e0ed95ef2fed9d'></a>market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='aadf50312fc554cc8ea5b66455390773'></a>market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e12b2149fb75315839afa5c8e759ea43'></a>market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6de1d1daa932e9d78fa50c2106434cc3'></a>market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='79609137a100d8b15e3ad53efa9a80d8'></a>market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a15170970cb1bd4059f01650cf884944'></a>market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2772b8324594f3f6cced978c8d6fb5f4'></a>market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='597cb0cc33f4aa6285b3f88ff97faabb'></a>market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ae2b070237006a424f3d3eb01f025f18'></a>market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9a98a107bea4c4d0b2751ff43bb26534'></a>market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        page,
        target_module,
        request_method,
        error
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='85ba5631727ffc41965edc3c8ba9e6c1'></a>market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b29f8e17da377677ed5de95f81ff8cf0'></a>market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b661e5c78ed72d38b1bde43638de1d4c'></a>market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='dfef6ddf234cfb246e218c345bc0c489'></a>market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        region,
        target_module,
        request_method,
        error
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4cab1dc706b33259fda63bebfc513bd0'></a>market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6993156f45497c51999cca71f93b1705'></a>market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8f22e0a6ff228eb52ab52374ec302190'></a>market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ca2f48f3c68764ec162f0cc193869619'></a>market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4a2322e3c82719a8835cd3b29d271770'></a>market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b2ee25a4162345c7b63d821d4ba5aa40'></a>market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8fabeadcba345be91d760f017a637593'></a>market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7f9971d85b88bfce739290ed62ba9516'></a>market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b07ba0a5d319f49924fe20f6facb6c3b'></a>market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b0b5095920751754fb7ea95fffbb4802'></a>market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ab996aca2fd385f6e0ad3ad709db6af2'></a>market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d8ccb102f6bc221b4d9f24cb38e73864'></a>market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9b4478a5f16283b0e305a062a403c6e3'></a>market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8329fb25c4a9fa01317da277b7ee33a0'></a>market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9422843d25939d85873b908a110061af'></a>market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f11195bd6ff5ba9b2f66c0c066d3d678'></a>market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4a7abf31bfecfc418689b12947ca6cd9'></a>market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c0aba132781c404f258550b1b7458be4'></a>market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6fc71a57527066cbcb2c39056bd235ff'></a>market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3699ae683f599c5bcc1f06adf2ca881f'></a>market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3dd2eae6e64917c48143f033ede4ef40'></a>market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6aaed0ffe7d1f128cc334b7eb9cbd961'></a>market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='69d801cc90e14855862a4f2be432527d'></a>market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='46b0b40b2eebb52ac7eaa33557893a95'></a>market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ac2e3841d37be7c4e2a40f7b8f6dce57'></a>market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b22e06248c46141a0d22142f867692d6'></a>market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.black_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_black_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```


## Overall Diagnostics

### Portion #1

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #3

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.black_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_black_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

