# market/nginx2/market_front_unified_b2b_fapi_errors
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `market_errors`

## Splits

```json
{
    "service_b2b_fapi": "transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' )",
    "level": "arrayJoin([level, 'any-level'])",
    "code": "replaceAll(code, '.', '_')",
    "dc": "multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' )",
    "host": "host",
    "type": "coalesce(nullIf(tags[1], ''), 'UNKNOWN')",
    "robot": "replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\\\)|MSRBOT \\\\(http://research\\\\.microsoft\\\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\\\.com|Refer\\\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '')",
    "requester": "multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\\\)|MSRBOT \\\\(http://research\\\\.microsoft\\\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\\\.com|Refer\\\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' )",
    "page": "replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_')",
    "region": "replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_')"
}
```

## Filters

```json
[
    "environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service'",
    "environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '' and page != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '' and page != ''"
]
```

## Resulting metrics

  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps`](#4cfa074c180fc25d87bc0884f2a40d00)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.splits.${dc}.${level}.${code}.metrics.hps`](#24962e3c68b9fdf692be7a63f8afaeb8)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps`](#e040dede0a22b7d9b064fc53337bac6a)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps`](#e80bbf106bb5b4c504970cb69e053b87)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.host.splits.${host}.${level}.${code}.metrics.hps`](#148b15cfcb6fc030141e31f78205fa9f)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps`](#c779faec991a5c1386346d69174b29fb)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.page.splits.${page}.${level}.${code}.metrics.hps`](#0977b0879497f146e22f6ddf7e43a087)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps`](#7787ffc4f6dc94947f402d492acede46)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps`](#7de4a8648e820e715c5bc8a9dbac1a1b)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps`](#4bb0bc6044a5a90304e983e10254937b)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.region.splits.${region}.${level}.${code}.metrics.hps`](#1e9a35dea341154a1d935eeed944902e)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps`](#ad204417103ee18f1ff349489ec09b3e)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps`](#47a47472d7db1fb5810816cde6ce0901)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps`](#9ed7fd883c7c9682d510957cb7c763a9)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps`](#7e1d7780a523b13481d846bce384f470)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.splits.${requester}.${level}.${code}.metrics.hps`](#57c70adeebe496560febbaeaad346829)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps`](#eaf1dabc2a6b3eaf59f760be37a797c2)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps`](#8bdf28ba9b21b0fe77aa7c61b81f29c4)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps`](#9abac9a96556f3edeb0db61772a93722)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps`](#21896281a0a69642ca14cef8357a40ad)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.splits.${robot}.${level}.${code}.metrics.hps`](#b740d6e24cd7787ebe4d0b2f3b847f5c)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps`](#1b2299d26752429006d9c934fc39a2d0)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.total.${level}.${code}.metrics.hps`](#56f87549a28ff0e45f1af5bd363f7f57)
  * [`market-front-unified.market_errors.v1.${service_b2b_fapi}.type.splits.${type}.${level}.${code}.metrics.hps`](#06f45a8a3b0ad9fdaa0e966daa8a94df)

## Metrics

#### <a id='56f87549a28ff0e45f1af5bd363f7f57'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.total.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.total.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.total.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='24962e3c68b9fdf692be7a63f8afaeb8'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.splits.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.dc.splits.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.splits.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='148b15cfcb6fc030141e31f78205fa9f'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.host.splits.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.host.splits.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.host.splits.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='06f45a8a3b0ad9fdaa0e966daa8a94df'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.type.splits.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.type.splits.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.type.splits.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='57c70adeebe496560febbaeaad346829'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.splits.${requester}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    requester,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.requester.splits.%24%7Brequester%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.splits.${requester}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        requester,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e040dede0a22b7d9b064fc53337bac6a'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    dc,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.dc.type.splits.%24%7Bdc%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        dc,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c779faec991a5c1386346d69174b29fb'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20host%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    host,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    host as host,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.host.type.splits.%24%7Bhost%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        host,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        host as host,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='eaf1dabc2a6b3eaf59f760be37a797c2'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    requester,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.requester.type.splits.%24%7Brequester%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        requester,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='47a47472d7db1fb5810816cde6ce0901'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    requester,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.requester.dc.splits.%24%7Brequester%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        requester,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9ed7fd883c7c9682d510957cb7c763a9'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    requester,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.requester.host.splits.%24%7Brequester%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        requester,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b740d6e24cd7787ebe4d0b2f3b847f5c'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.splits.${robot}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    robot,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.robot.splits.%24%7Brobot%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.splits.${robot}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        robot,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1b2299d26752429006d9c934fc39a2d0'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    robot,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.robot.type.splits.%24%7Brobot%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        robot,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8bdf28ba9b21b0fe77aa7c61b81f29c4'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    robot,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.robot.dc.splits.%24%7Brobot%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        robot,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9abac9a96556f3edeb0db61772a93722'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    robot,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.robot.host.splits.%24%7Brobot%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        robot,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0977b0879497f146e22f6ddf7e43a087'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.page.splits.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.page.splits.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.page.splits.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4cfa074c180fc25d87bc0884f2a40d00'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    dc,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.dc.page.splits.%24%7Bdc%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        dc,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e80bbf106bb5b4c504970cb69e053b87'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20host%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    host,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    host as host,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.host.page.splits.%24%7Bhost%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        host,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        host as host,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7e1d7780a523b13481d846bce384f470'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    requester,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.requester.page.splits.%24%7Brequester%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        requester,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1e9a35dea341154a1d935eeed944902e'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.region.splits.${region}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20region%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    region,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.region.splits.%24%7Bregion%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.region.splits.${region}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        region,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ad204417103ee18f1ff349489ec09b3e'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20region%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    region,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.region.type.splits.%24%7Bregion%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        region,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7787ffc4f6dc94947f402d492acede46'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20region%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    region,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.region.dc.splits.%24%7Bregion%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        region,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7de4a8648e820e715c5bc8a9dbac1a1b'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20region%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    region,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.region.host.splits.%24%7Bregion%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        region,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='21896281a0a69642ca14cef8357a40ad'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20''%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    robot,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.robot.page.splits.%24%7Brobot%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20''%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        robot,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4bb0bc6044a5a90304e983e10254937b'></a>market-front-unified.market_errors.v1.${service_b2b_fapi}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20region%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20region%20!%3D%20''%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_b2b_fapi,
    region,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_b2b_fapi%7D.region.page.splits.%24%7Bregion%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_b2b_fapi%20!%3D%20'undefined_service'%20and%20region%20!%3D%20''%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_b2b-fapi'%5D%2C%20%5B'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_b2b_fapi%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_b2b_fapi}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_b2b_fapi,
        region,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```


## Overall Diagnostics

### Portion #1

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.total.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.splits.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.host.splits.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.type.splits.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.splits.${requester}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, requester, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, dc, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, host, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, host as host, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, requester, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, requester, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, requester, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.splits.${robot}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, robot, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, robot, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, robot, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, robot, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.page.splits.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, dc, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, host, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, host as host, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, requester, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.region.splits.${region}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, region, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, region, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, region, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, region, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, robot, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and robot != '' and page != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_b2b_fapi}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_b2b_fapi, region, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_b2b_fapi != 'undefined_service' and region != '' and page != '') GROUP BY metric_ts, transform(service, ['market_b2b-fapi'], ['b2b_fapi'], 'undefined_service' ) as service_b2b_fapi, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

