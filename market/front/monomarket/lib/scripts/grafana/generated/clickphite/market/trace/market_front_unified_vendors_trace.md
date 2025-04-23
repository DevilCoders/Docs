# market/trace/market_front_unified_vendors_trace
    
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
    "environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_vendors'",
    "environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != ''",
    "environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_vendors' and region != ''"
]
```

## Resulting metrics

  * [`market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#3c99d797f0faa32a3755f91fe91bcb94)
  * [`market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps`](#674a9c09bfe4ac1bd951a63b4bb0bc6e)
  * [`market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#765ce5d96b2f50e68a9b8df063783b7e)
  * [`market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#6fac4655bf4857e8cd70de2b7ce5a047)
  * [`market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps`](#4724cdd0e06cdd871a68f07f107ff46b)
  * [`market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#7a5f21a2a0d8c559a81049db8257513d)
  * [`market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps`](#be8366941e16612f0a5fed44e920247f)
  * [`market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#a6813273e2c059ee1953c900027e8bd8)
  * [`market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#6327a408dad76a816f0fd3bf9bc82b91)
  * [`market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps`](#fee27442a690568c202512b38e01e744)
  * [`market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#d4ae24bc4093589b2be98b06630e63dc)
  * [`market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#36f6a5b548c2d864c9d0845056827a60)
  * [`market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps`](#81577b4c867615a61461e8b641b83036)
  * [`market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#84ad5ec9a7a3c3004de6b7a10045f3d9)
  * [`market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps`](#9d3981b600096b947571b98e43aa05d9)
  * [`market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#01b337c9aa844013bacb1d1ea0394595)
  * [`market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#817406cc77d51ee4138772873981b204)
  * [`market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps`](#b1b9b7a44c0c9d2ffc645f30b8dacaac)
  * [`market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#1169825164d91ca170c6b5f029614b63)
  * [`market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#0b02aa287a2ec5aa47a6cfb31ca746d8)
  * [`market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps`](#67d8bd5b42849b300e89beb4f9a2bb96)
  * [`market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#714afcd2e7bfb30d04353b0784e8ebd6)
  * [`market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps`](#a6ebcb4688a269519a2d00858a2db3ac)
  * [`market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#a4056f0fcfd79dfef8d9711f21187aec)
  * [`market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#4756840fe222edbd233c20f6194c1c5f)
  * [`market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps`](#d4ffa6be07068c500bf88d858b95a6ad)
  * [`market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#dccda747d5c78c5f97212a0705688908)
  * [`market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#8cd38ad8aadde6a6a583257588533e17)
  * [`market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps`](#9ddbec091d5d7da5abbff50dfc1ec21a)
  * [`market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#d095024d838fc9ae2c7884b8abc895ba)
  * [`market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps`](#833f5e6bd6d4b28085065d6be385ba5d)
  * [`market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#853d6fdd7ac518cf7c14c22bd89e0d1b)
  * [`market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#fa4bfe385df1f313b9d78ac3ecf4c1aa)
  * [`market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps`](#6dcba69f884fb35c965148a7b9dfb8f1)
  * [`market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#b4f29d932700f21fa13e3c3a2e086586)
  * [`market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#19ded9762bdcf83b0e98e8d3cdad38b7)
  * [`market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps`](#c41ddfee423203bd7bcb7c561b54ef0c)
  * [`market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#b4fc08074f802b76fc74c294ca222687)
  * [`market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps`](#df4bb2028e9f8387f9bc4cab80e11260)
  * [`market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#de27f6e2fed7491907f1f9bc1de6ef96)
  * [`market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#c8a075be51de101c5a6d4339390481f6)
  * [`market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps`](#fa0f8bb9e9557da0e39d5e68f9bac576)
  * [`market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#0d014b4bf21847bb88a04140d8056770)
  * [`market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#1034670d6e128aab1d4bb7ef15cd7c08)
  * [`market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps`](#7fa57c2c8746fcfabf637737da43d4da)
  * [`market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#4457d84fbeb0bfb5087c215136b7abe5)
  * [`market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps`](#8185573e3340302c68a3b4aca2cb6784)
  * [`market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#18c858c9698bc8a9462aa9470758dbb8)

## Metrics

#### <a id='8185573e3340302c68a3b4aca2cb6784'></a>market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='18c858c9698bc8a9462aa9470758dbb8'></a>market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='be8366941e16612f0a5fed44e920247f'></a>market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a6813273e2c059ee1953c900027e8bd8'></a>market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')
    
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
#### <a id='9d3981b600096b947571b98e43aa05d9'></a>market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='01b337c9aa844013bacb1d1ea0394595'></a>market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')
    
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
#### <a id='df4bb2028e9f8387f9bc4cab80e11260'></a>market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='de27f6e2fed7491907f1f9bc1de6ef96'></a>market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '')
    
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
#### <a id='7fa57c2c8746fcfabf637737da43d4da'></a>market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fa0f8bb9e9557da0e39d5e68f9bac576'></a>market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4724cdd0e06cdd871a68f07f107ff46b'></a>market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='674a9c09bfe4ac1bd951a63b4bb0bc6e'></a>market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
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
#### <a id='81577b4c867615a61461e8b641b83036'></a>market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fee27442a690568c202512b38e01e744'></a>market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
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
#### <a id='c41ddfee423203bd7bcb7c561b54ef0c'></a>market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6dcba69f884fb35c965148a7b9dfb8f1'></a>market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
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
#### <a id='a6ebcb4688a269519a2d00858a2db3ac'></a>market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a4056f0fcfd79dfef8d9711f21187aec'></a>market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '' and error_code != '')
    
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
#### <a id='67d8bd5b42849b300e89beb4f9a2bb96'></a>market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b1b9b7a44c0c9d2ffc645f30b8dacaac'></a>market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')
    
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
#### <a id='833f5e6bd6d4b28085065d6be385ba5d'></a>market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='853d6fdd7ac518cf7c14c22bd89e0d1b'></a>market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '' and error_code != '')
    
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
#### <a id='9ddbec091d5d7da5abbff50dfc1ec21a'></a>market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d4ffa6be07068c500bf88d858b95a6ad'></a>market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')
    
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
#### <a id='4457d84fbeb0bfb5087c215136b7abe5'></a>market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0d014b4bf21847bb88a04140d8056770'></a>market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7a5f21a2a0d8c559a81049db8257513d'></a>market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='765ce5d96b2f50e68a9b8df063783b7e'></a>market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
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
#### <a id='84ad5ec9a7a3c3004de6b7a10045f3d9'></a>market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d4ae24bc4093589b2be98b06630e63dc'></a>market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
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
#### <a id='b4fc08074f802b76fc74c294ca222687'></a>market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b4f29d932700f21fa13e3c3a2e086586'></a>market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
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
#### <a id='714afcd2e7bfb30d04353b0784e8ebd6'></a>market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1169825164d91ca170c6b5f029614b63'></a>market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')
    
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
#### <a id='d095024d838fc9ae2c7884b8abc895ba'></a>market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='dccda747d5c78c5f97212a0705688908'></a>market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')
    
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
#### <a id='1034670d6e128aab1d4bb7ef15cd7c08'></a>market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c8a075be51de101c5a6d4339390481f6'></a>market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6fac4655bf4857e8cd70de2b7ce5a047'></a>market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3c99d797f0faa32a3755f91fe91bcb94'></a>market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
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
#### <a id='36f6a5b548c2d864c9d0845056827a60'></a>market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6327a408dad76a816f0fd3bf9bc82b91'></a>market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
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
#### <a id='19ded9762bdcf83b0e98e8d3cdad38b7'></a>market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fa4bfe385df1f313b9d78ac3ecf4c1aa'></a>market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors')
    
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
#### <a id='0b02aa287a2ec5aa47a6cfb31ca746d8'></a>market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='817406cc77d51ee4138772873981b204'></a>market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '')
    
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
#### <a id='8cd38ad8aadde6a6a583257588533e17'></a>market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4756840fe222edbd233c20f6194c1c5f'></a>market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.vendors_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_vendors'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '')
    
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
    SELECT 'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #3

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.vendors_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_vendors' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

