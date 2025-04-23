# market/nginx2/market_front_unified_b2b_fapi_trace
    
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
    "environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_b2b-fapi'",
    "environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != ''",
    "environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != ''"
]
```

## Resulting metrics

  * [`market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#73a1035b80c5aa6b7bd55e07b1e6e44b)
  * [`market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps`](#810ba03f8dbc0251502ef0d74b6dfd74)
  * [`market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#203aecf6687db08385e5494de6989ab7)
  * [`market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#dbdafa55a20d932039d31f0699679e0f)
  * [`market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps`](#26ad59a622a45f7058c1524dfa6eca42)
  * [`market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#a5ec424f050676c5af62401f2af73700)
  * [`market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps`](#83b8bf358d3e88b3b1519029e4267041)
  * [`market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#a497a52e0dbc675b8dda22733bf840ed)
  * [`market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#671d37dbeb4157e3c0940ad84741f370)
  * [`market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps`](#59cca38ad4f0dd908f833ca734ec76ab)
  * [`market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#9269c70602d4c699627226028cbc85c9)
  * [`market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#a28efb0c1176e2225360e98e783394c8)
  * [`market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps`](#80f1677e6b1c032e9fdfa2b35c8235a6)
  * [`market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#3febff821fea1fe8025fb49c3109c0bd)
  * [`market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps`](#a5f488a3b0fd4f894dd8306a7aca06a3)
  * [`market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#6ff0d409493622e5f5474ad2ed27d2fa)
  * [`market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#a4ca1bdb7c250a499d14da7650c251d3)
  * [`market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps`](#80cf5feea211abbe837d9c62dd81f681)
  * [`market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#add4ef85c32fc46764a715a0bc2927d4)
  * [`market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#f9d4710cbbda0e7d09f1f817552b4c7e)
  * [`market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps`](#6b5f016fa50d64be1eda2dad3abe0f10)
  * [`market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#59e4984393cd039cff82b2c8e577c623)
  * [`market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps`](#95eccdf77f7eeaca0a0547cab3a36327)
  * [`market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#c07f51c510d1f3f692f69782003c2c0d)
  * [`market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#bff143785137f2b5e4e822d929ec6fcd)
  * [`market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps`](#60daffc2841c7c006235ec95a678f798)
  * [`market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#9e5f9ba48ebca2da6f7cc66fe1132cec)
  * [`market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#60b3882e60644451e8b137c172a059e2)
  * [`market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps`](#6336346fc1951bacfa6d728a4170a39c)
  * [`market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#c6335615620d4da35fd202c7c4909153)
  * [`market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps`](#4da4532f055c056a8600f5a9984a4134)
  * [`market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#6b20524d739687dcc5060de5eff0ec2d)
  * [`market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#997846e17fd1b77f411fef0318a2e2d2)
  * [`market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps`](#6aa34a99dc0e31fdd8f3ea706f579fd7)
  * [`market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#bf6c313d3370fb10864026164b71804b)
  * [`market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#bd64bc4b5ce864c6fd39d68eaa4d7f35)
  * [`market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps`](#a432dc7af190c20fe1d33add5de9832f)
  * [`market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#d316b2b2ddbee24fc2e13f0939071a8b)
  * [`market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps`](#7767c3917b9aa8ac487d4bf020c39fb8)
  * [`market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#3f7435f646bceecad09e1cf74394bf28)
  * [`market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#fd884cf46fe34c52e8c638045156c6ce)
  * [`market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.rps`](#bd74203220e9e6a0c5669de4866374a7)
  * [`market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#7852bcbf1b426515154ddb8264d718d7)
  * [`market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#5149d1bc5a8befeb94e63f90d918570f)
  * [`market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.rps`](#2c4743e54ec33f5f55b030c9ef1ce51e)
  * [`market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#3e6b912717f11159f24ee62857ea786e)
  * [`market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.error.any-error.metrics.rps`](#496c638d5d5870b222613b82400a5bae)
  * [`market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#e7a3728f6db9bc4e205481ead88c77a7)

## Metrics

#### <a id='496c638d5d5870b222613b82400a5bae'></a>market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e7a3728f6db9bc4e205481ead88c77a7'></a>market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='83b8bf358d3e88b3b1519029e4267041'></a>market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a497a52e0dbc675b8dda22733bf840ed'></a>market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')
    
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
#### <a id='a5f488a3b0fd4f894dd8306a7aca06a3'></a>market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6ff0d409493622e5f5474ad2ed27d2fa'></a>market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')
    
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
#### <a id='7767c3917b9aa8ac487d4bf020c39fb8'></a>market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3f7435f646bceecad09e1cf74394bf28'></a>market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '')
    
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
#### <a id='2c4743e54ec33f5f55b030c9ef1ce51e'></a>market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bd74203220e9e6a0c5669de4866374a7'></a>market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='26ad59a622a45f7058c1524dfa6eca42'></a>market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='810ba03f8dbc0251502ef0d74b6dfd74'></a>market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
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
#### <a id='80f1677e6b1c032e9fdfa2b35c8235a6'></a>market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='59cca38ad4f0dd908f833ca734ec76ab'></a>market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
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
#### <a id='a432dc7af190c20fe1d33add5de9832f'></a>market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6aa34a99dc0e31fdd8f3ea706f579fd7'></a>market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
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
#### <a id='95eccdf77f7eeaca0a0547cab3a36327'></a>market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c07f51c510d1f3f692f69782003c2c0d'></a>market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '' and error_code != '')
    
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
#### <a id='6b5f016fa50d64be1eda2dad3abe0f10'></a>market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='80cf5feea211abbe837d9c62dd81f681'></a>market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')
    
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
#### <a id='4da4532f055c056a8600f5a9984a4134'></a>market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6b20524d739687dcc5060de5eff0ec2d'></a>market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '' and error_code != '')
    
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
#### <a id='6336346fc1951bacfa6d728a4170a39c'></a>market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='60daffc2841c7c006235ec95a678f798'></a>market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')
    
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
#### <a id='3e6b912717f11159f24ee62857ea786e'></a>market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7852bcbf1b426515154ddb8264d718d7'></a>market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a5ec424f050676c5af62401f2af73700'></a>market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='203aecf6687db08385e5494de6989ab7'></a>market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
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
#### <a id='3febff821fea1fe8025fb49c3109c0bd'></a>market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9269c70602d4c699627226028cbc85c9'></a>market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
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
#### <a id='d316b2b2ddbee24fc2e13f0939071a8b'></a>market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bf6c313d3370fb10864026164b71804b'></a>market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
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
#### <a id='59e4984393cd039cff82b2c8e577c623'></a>market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='add4ef85c32fc46764a715a0bc2927d4'></a>market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')
    
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
#### <a id='c6335615620d4da35fd202c7c4909153'></a>market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9e5f9ba48ebca2da6f7cc66fe1132cec'></a>market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')
    
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
#### <a id='5149d1bc5a8befeb94e63f90d918570f'></a>market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fd884cf46fe34c52e8c638045156c6ce'></a>market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='dbdafa55a20d932039d31f0699679e0f'></a>market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='73a1035b80c5aa6b7bd55e07b1e6e44b'></a>market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
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
#### <a id='a28efb0c1176e2225360e98e783394c8'></a>market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='671d37dbeb4157e3c0940ad84741f370'></a>market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
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
#### <a id='bd64bc4b5ce864c6fd39d68eaa4d7f35'></a>market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='997846e17fd1b77f411fef0318a2e2d2'></a>market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi')
    
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
#### <a id='f9d4710cbbda0e7d09f1f817552b4c7e'></a>market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a4ca1bdb7c250a499d14da7650c251d3'></a>market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '')
    
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
#### <a id='60b3882e60644451e8b137c172a059e2'></a>market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bff143785137f2b5e4e822d929ec6fcd'></a>market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.b2b_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_b2b-fapi'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '')
    
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
    SELECT 'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #3

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.b2b_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_b2b-fapi' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

