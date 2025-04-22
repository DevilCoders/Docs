# market/nginx2/market_front_unified_black_errors
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `market_errors`

## Splits

```json
{
    "service_black": "transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' )",
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
    "environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service'",
    "environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '' and page != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '' and page != ''"
]
```

## Resulting metrics

  * [`market-front-unified.market_errors.v1.${service_black}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps`](#c0ea395c64ee3300e34a1933305c4e1e)
  * [`market-front-unified.market_errors.v1.${service_black}.dc.splits.${dc}.${level}.${code}.metrics.hps`](#339fd9aff5b0cb80abfc9124f51503a7)
  * [`market-front-unified.market_errors.v1.${service_black}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps`](#7a5b01e0832a225a4c3eb4f257313bb4)
  * [`market-front-unified.market_errors.v1.${service_black}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps`](#ed32d866fb431ee349380124797b2b11)
  * [`market-front-unified.market_errors.v1.${service_black}.host.splits.${host}.${level}.${code}.metrics.hps`](#f10b991c0568c98fc27dcde26d48e16d)
  * [`market-front-unified.market_errors.v1.${service_black}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps`](#f880d53d5e88b61d850a215a3a3bbbe9)
  * [`market-front-unified.market_errors.v1.${service_black}.page.splits.${page}.${level}.${code}.metrics.hps`](#db758c6c90cb8f6c59eb0ab945e33892)
  * [`market-front-unified.market_errors.v1.${service_black}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps`](#9147f6d31bbe755708950bbe0c7d8ab3)
  * [`market-front-unified.market_errors.v1.${service_black}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps`](#e87a3aa5514d247efef19fe61fb1b397)
  * [`market-front-unified.market_errors.v1.${service_black}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps`](#c4029e1c7b8dcfa92f130cafa4404862)
  * [`market-front-unified.market_errors.v1.${service_black}.region.splits.${region}.${level}.${code}.metrics.hps`](#f5f614a964bc88909a1e7de216205feb)
  * [`market-front-unified.market_errors.v1.${service_black}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps`](#5cdd0a6442212c0ddb91083449264d7e)
  * [`market-front-unified.market_errors.v1.${service_black}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps`](#cf49c8d19070582ae263c057f4d513f7)
  * [`market-front-unified.market_errors.v1.${service_black}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps`](#c4cf1c370becd834b1eaeda9b3aded1b)
  * [`market-front-unified.market_errors.v1.${service_black}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps`](#15f513e75a1ca53d4608af69ab717860)
  * [`market-front-unified.market_errors.v1.${service_black}.requester.splits.${requester}.${level}.${code}.metrics.hps`](#84c06d1e6ba1c76a454190f46952264f)
  * [`market-front-unified.market_errors.v1.${service_black}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps`](#a84bf15f66822e7f4a1df3bc2ddc3f34)
  * [`market-front-unified.market_errors.v1.${service_black}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps`](#dc87cda938c6c96ad629e094d6c3cd04)
  * [`market-front-unified.market_errors.v1.${service_black}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps`](#98e749a2addf9fd786ef9e104ef1761a)
  * [`market-front-unified.market_errors.v1.${service_black}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps`](#9d6a419a79e7bdbd1bdc3acc54d3f1dc)
  * [`market-front-unified.market_errors.v1.${service_black}.robot.splits.${robot}.${level}.${code}.metrics.hps`](#c79e1b182e6d6213f2799acd9e9362ac)
  * [`market-front-unified.market_errors.v1.${service_black}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps`](#45d83ae554f1d731891df0da1676f4be)
  * [`market-front-unified.market_errors.v1.${service_black}.total.${level}.${code}.metrics.hps`](#19cc31bc83598d3a6f836ef74fed9a32)
  * [`market-front-unified.market_errors.v1.${service_black}.type.splits.${type}.${level}.${code}.metrics.hps`](#ec3e9a5b91dce9ac264b16c7cacfaaab)

## Metrics

#### <a id='19cc31bc83598d3a6f836ef74fed9a32'></a>market-front-unified.market_errors.v1.${service_black}.total.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.total.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.total.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='339fd9aff5b0cb80abfc9124f51503a7'></a>market-front-unified.market_errors.v1.${service_black}.dc.splits.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.dc.splits.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.dc.splits.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f10b991c0568c98fc27dcde26d48e16d'></a>market-front-unified.market_errors.v1.${service_black}.host.splits.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.host.splits.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.host.splits.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ec3e9a5b91dce9ac264b16c7cacfaaab'></a>market-front-unified.market_errors.v1.${service_black}.type.splits.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.type.splits.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.type.splits.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='84c06d1e6ba1c76a454190f46952264f'></a>market-front-unified.market_errors.v1.${service_black}.requester.splits.${requester}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.requester.splits.${requester}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7a5b01e0832a225a4c3eb4f257313bb4'></a>market-front-unified.market_errors.v1.${service_black}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    dc,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.dc.type.splits.%24%7Bdc%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        dc,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f880d53d5e88b61d850a215a3a3bbbe9'></a>market-front-unified.market_errors.v1.${service_black}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20host%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    host,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    host as host,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.host.type.splits.%24%7Bhost%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        host,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        host as host,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a84bf15f66822e7f4a1df3bc2ddc3f34'></a>market-front-unified.market_errors.v1.${service_black}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.requester.type.splits.%24%7Brequester%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='cf49c8d19070582ae263c057f4d513f7'></a>market-front-unified.market_errors.v1.${service_black}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.requester.dc.splits.%24%7Brequester%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c4cf1c370becd834b1eaeda9b3aded1b'></a>market-front-unified.market_errors.v1.${service_black}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.requester.host.splits.%24%7Brequester%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c79e1b182e6d6213f2799acd9e9362ac'></a>market-front-unified.market_errors.v1.${service_black}.robot.splits.${robot}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robot,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.robot.splits.%24%7Brobot%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.robot.splits.${robot}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robot,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='45d83ae554f1d731891df0da1676f4be'></a>market-front-unified.market_errors.v1.${service_black}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robot,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.robot.type.splits.%24%7Brobot%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robot,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='dc87cda938c6c96ad629e094d6c3cd04'></a>market-front-unified.market_errors.v1.${service_black}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robot,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.robot.dc.splits.%24%7Brobot%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robot,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='98e749a2addf9fd786ef9e104ef1761a'></a>market-front-unified.market_errors.v1.${service_black}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robot,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.robot.host.splits.%24%7Brobot%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robot,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='db758c6c90cb8f6c59eb0ab945e33892'></a>market-front-unified.market_errors.v1.${service_black}.page.splits.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.page.splits.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.page.splits.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c0ea395c64ee3300e34a1933305c4e1e'></a>market-front-unified.market_errors.v1.${service_black}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    dc,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.dc.page.splits.%24%7Bdc%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        dc,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ed32d866fb431ee349380124797b2b11'></a>market-front-unified.market_errors.v1.${service_black}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20host%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    host,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    host as host,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.host.page.splits.%24%7Bhost%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        host,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        host as host,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='15f513e75a1ca53d4608af69ab717860'></a>market-front-unified.market_errors.v1.${service_black}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.requester.page.splits.%24%7Brequester%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f5f614a964bc88909a1e7de216205feb'></a>market-front-unified.market_errors.v1.${service_black}.region.splits.${region}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20region%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    region,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.region.splits.%24%7Bregion%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.region.splits.${region}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        region,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5cdd0a6442212c0ddb91083449264d7e'></a>market-front-unified.market_errors.v1.${service_black}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20region%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    region,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.region.type.splits.%24%7Bregion%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        region,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9147f6d31bbe755708950bbe0c7d8ab3'></a>market-front-unified.market_errors.v1.${service_black}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20region%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    region,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.region.dc.splits.%24%7Bregion%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        region,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e87a3aa5514d247efef19fe61fb1b397'></a>market-front-unified.market_errors.v1.${service_black}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20region%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    region,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.region.host.splits.%24%7Bregion%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        region,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9d6a419a79e7bdbd1bdc3acc54d3f1dc'></a>market-front-unified.market_errors.v1.${service_black}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20''%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robot,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.robot.page.splits.%24%7Brobot%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20''%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robot,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c4029e1c7b8dcfa92f130cafa4404862'></a>market-front-unified.market_errors.v1.${service_black}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20region%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20region%20!%3D%20''%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    region,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_black%7D.region.page.splits.%24%7Bregion%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_black%20!%3D%20'undefined_service'%20and%20region%20!%3D%20''%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_black_desktop'%5D%2C%20%5B'black_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_black}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        region,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black,
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
    SELECT 'market-front-unified.market_errors.v1.${service_black}.total.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.dc.splits.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.host.splits.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.type.splits.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.requester.splits.${requester}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, dc, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, host, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, host as host, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.robot.splits.${robot}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robot, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robot, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robot, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robot, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.page.splits.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, dc, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, host, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, host as host, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.region.splits.${region}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, region, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, region, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_errors.v1.${service_black}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, region, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, region, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robot, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and robot != '' and page != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_black}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, region, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_black != 'undefined_service' and region != '' and page != '') GROUP BY metric_ts, transform(service, ['market_front_black_desktop'], ['black_desktop'], 'undefined_service' ) as service_black, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

