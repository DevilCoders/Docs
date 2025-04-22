# market/trace/market_front_unified_corpsite_trace
    
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
    "environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_marketcorp'",
    "environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != ''",
    "environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != ''"
]
```

## Resulting metrics

  * [`market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#4bd8e24e1468091f7b0f479f6f6e16a0)
  * [`market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps`](#6fc68031901b5ae711b9db0ef8321d5d)
  * [`market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#77ab8fceaaafe652d303bbe8043d42d1)
  * [`market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#257b2aa5b64a74c7a7926652f13afb2a)
  * [`market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps`](#4b68848231d52c9635b328d1d47c4096)
  * [`market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#2631695357a58918833ea3bea911d8bf)
  * [`market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps`](#d796c2dd5c297598037e5b4b3aaa937e)
  * [`market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#dc8ee2fb283595f289730c094f8ea640)
  * [`market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#687bb30a2397b550c3b0b14f6352f2b7)
  * [`market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps`](#05069679ab727dc54c8f416b730eec7f)
  * [`market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#047706cfd37015b7cb6a0056341c4388)
  * [`market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#2cb76b7211809070e79cb961bd5439f6)
  * [`market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps`](#798306da6c3972367212eeb9384f30d7)
  * [`market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#4dbc9bd6092c508b3e44383fe36479d4)
  * [`market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps`](#4d53cf9dd820527771ad07b20c9e6a6d)
  * [`market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#52eaa6f81532aaa2f7012c6522f26728)
  * [`market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#9bfba582b5b53de1a55c2270becface9)
  * [`market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps`](#4eea74b204be0f75d48a441c5cad063e)
  * [`market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#19b42432b9efd863558d49eca9bd836b)
  * [`market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#c2a997a4321482e6ebfb35d8d1f4a17e)
  * [`market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps`](#ef4ea2ca1e5c604adaa4a331d0a7aae5)
  * [`market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#c1ead04442311f830e1905fe447da8fe)
  * [`market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps`](#d06ec7c31dea02d611416f912c331fe1)
  * [`market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#bdb3269a81d75cb26556ce1b670362ed)
  * [`market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#976545e725dc19e08fb5eded07cbc286)
  * [`market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps`](#f9a322ec0c4ecb92f590ee5911312645)
  * [`market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#8797d4007e930e703fd4a232aed0cb53)
  * [`market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#f7ae7843221331f2b6b7284dd36bc278)
  * [`market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps`](#22da459a693eceb4b45a433809ad25be)
  * [`market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#d443f6aa1a23d84f1b262327eb20df6c)
  * [`market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps`](#6c5d90560a5c2e0a163cec31a458fb0c)
  * [`market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#04a194ff75857f0abdde0d4cf75a8591)
  * [`market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#445b996d3b9398ddad6a0c6481ed0d28)
  * [`market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps`](#10a6aedd26022b97ea1304c7bb60be3b)
  * [`market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#4733eb2ca97dd56f1ae9038d4d36de1f)
  * [`market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#e2d00cc09af9366b5817fcd618de4d3f)
  * [`market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps`](#6cba78bcbdc47a47added0fa4299df3a)
  * [`market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#a839403be18ebc7481fa21aacfacc940)
  * [`market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps`](#731caf092bf071dbb55b522cb84546db)
  * [`market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#023f05547b9f44154633d41be06eb9a5)
  * [`market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#b09d232b13f77f5e8954312d8dda7c53)
  * [`market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps`](#1d70d5dd80e9093a4d83388c57ba1669)
  * [`market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#018b11fb1d3000493c50726fd95a78c5)
  * [`market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#dc64ee0ae1852879d2301fef8830022e)
  * [`market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps`](#3518ee0e0c3f49512ba7545a1c603561)
  * [`market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#a4fe3c3b3b1055658797b4e0ed054bbe)
  * [`market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps`](#ee7d4e154a1092c922a22837895ad402)
  * [`market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#9c051ec7b7e6db103e67b399de6a5bb9)

## Metrics

#### <a id='ee7d4e154a1092c922a22837895ad402'></a>market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9c051ec7b7e6db103e67b399de6a5bb9'></a>market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d796c2dd5c297598037e5b4b3aaa937e'></a>market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='dc8ee2fb283595f289730c094f8ea640'></a>market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')
    
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
#### <a id='4d53cf9dd820527771ad07b20c9e6a6d'></a>market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='52eaa6f81532aaa2f7012c6522f26728'></a>market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')
    
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
#### <a id='731caf092bf071dbb55b522cb84546db'></a>market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='023f05547b9f44154633d41be06eb9a5'></a>market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '')
    
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
#### <a id='3518ee0e0c3f49512ba7545a1c603561'></a>market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1d70d5dd80e9093a4d83388c57ba1669'></a>market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4b68848231d52c9635b328d1d47c4096'></a>market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6fc68031901b5ae711b9db0ef8321d5d'></a>market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
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
#### <a id='798306da6c3972367212eeb9384f30d7'></a>market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='05069679ab727dc54c8f416b730eec7f'></a>market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
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
#### <a id='6cba78bcbdc47a47added0fa4299df3a'></a>market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='10a6aedd26022b97ea1304c7bb60be3b'></a>market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
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
#### <a id='d06ec7c31dea02d611416f912c331fe1'></a>market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bdb3269a81d75cb26556ce1b670362ed'></a>market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '' and error_code != '')
    
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
#### <a id='ef4ea2ca1e5c604adaa4a331d0a7aae5'></a>market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4eea74b204be0f75d48a441c5cad063e'></a>market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')
    
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
#### <a id='6c5d90560a5c2e0a163cec31a458fb0c'></a>market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='04a194ff75857f0abdde0d4cf75a8591'></a>market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '' and error_code != '')
    
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
#### <a id='22da459a693eceb4b45a433809ad25be'></a>market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f9a322ec0c4ecb92f590ee5911312645'></a>market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')
    
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
#### <a id='a4fe3c3b3b1055658797b4e0ed054bbe'></a>market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='018b11fb1d3000493c50726fd95a78c5'></a>market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2631695357a58918833ea3bea911d8bf'></a>market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='77ab8fceaaafe652d303bbe8043d42d1'></a>market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
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
#### <a id='4dbc9bd6092c508b3e44383fe36479d4'></a>market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='047706cfd37015b7cb6a0056341c4388'></a>market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
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
#### <a id='a839403be18ebc7481fa21aacfacc940'></a>market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4733eb2ca97dd56f1ae9038d4d36de1f'></a>market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
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
#### <a id='c1ead04442311f830e1905fe447da8fe'></a>market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='19b42432b9efd863558d49eca9bd836b'></a>market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')
    
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
#### <a id='d443f6aa1a23d84f1b262327eb20df6c'></a>market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8797d4007e930e703fd4a232aed0cb53'></a>market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')
    
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
#### <a id='dc64ee0ae1852879d2301fef8830022e'></a>market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b09d232b13f77f5e8954312d8dda7c53'></a>market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='257b2aa5b64a74c7a7926652f13afb2a'></a>market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4bd8e24e1468091f7b0f479f6f6e16a0'></a>market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
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
#### <a id='2cb76b7211809070e79cb961bd5439f6'></a>market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='687bb30a2397b550c3b0b14f6352f2b7'></a>market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
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
#### <a id='e2d00cc09af9366b5817fcd618de4d3f'></a>market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='445b996d3b9398ddad6a0c6481ed0d28'></a>market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp')
    
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
#### <a id='c2a997a4321482e6ebfb35d8d1f4a17e'></a>market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9bfba582b5b53de1a55c2270becface9'></a>market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '')
    
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
#### <a id='f7ae7843221331f2b6b7284dd36bc278'></a>market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='976545e725dc19e08fb5eded07cbc286'></a>market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.corpsite_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_marketcorp'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '')
    
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
    SELECT 'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #3

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.corpsite_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_marketcorp' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

