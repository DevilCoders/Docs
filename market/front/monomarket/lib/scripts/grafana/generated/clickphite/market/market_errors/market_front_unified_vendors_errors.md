# market/market_errors/market_front_unified_vendors_errors
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `market_errors`

## Splits

```json
{
    "service_vendors": "transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' )",
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
    "environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service'",
    "environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '' and page != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '' and page != ''"
]
```

## Resulting metrics

  * [`market-front-unified.market_errors.v1.${service_vendors}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps`](#7c2cbf87d47bb60d54cfb050e2dcb205)
  * [`market-front-unified.market_errors.v1.${service_vendors}.dc.splits.${dc}.${level}.${code}.metrics.hps`](#8b076453d25f238c44b518a9162de5d0)
  * [`market-front-unified.market_errors.v1.${service_vendors}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps`](#ec4977f1de99eae94fbb3051749859ad)
  * [`market-front-unified.market_errors.v1.${service_vendors}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps`](#d5d00f33ebf7b94cedbfb973810e8cb3)
  * [`market-front-unified.market_errors.v1.${service_vendors}.host.splits.${host}.${level}.${code}.metrics.hps`](#7cb818974a43fa4aee62d66ced3ddd08)
  * [`market-front-unified.market_errors.v1.${service_vendors}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps`](#ee1853a37a4aa7be659bddf0a23eeb1b)
  * [`market-front-unified.market_errors.v1.${service_vendors}.page.splits.${page}.${level}.${code}.metrics.hps`](#4b14192f33225b1edb4cc3b9cbe0c87b)
  * [`market-front-unified.market_errors.v1.${service_vendors}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps`](#477408b9b2152fe5026b560a0d85eb3b)
  * [`market-front-unified.market_errors.v1.${service_vendors}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps`](#f0a7281165c231b41df2149913ed55ce)
  * [`market-front-unified.market_errors.v1.${service_vendors}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps`](#00f858aa5dd97615cb32c24214fc5695)
  * [`market-front-unified.market_errors.v1.${service_vendors}.region.splits.${region}.${level}.${code}.metrics.hps`](#be04bd2ad8cad31b2449621c6e9aa017)
  * [`market-front-unified.market_errors.v1.${service_vendors}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps`](#af546798dc6840c8cf8f67c785831842)
  * [`market-front-unified.market_errors.v1.${service_vendors}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps`](#21fd4cd8c6a779b0a585cdeb4cf6b10c)
  * [`market-front-unified.market_errors.v1.${service_vendors}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps`](#9ff303924da56c14fa3db404228a5da4)
  * [`market-front-unified.market_errors.v1.${service_vendors}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps`](#06501fa7f15116cb2ae0b3ce1e4349ca)
  * [`market-front-unified.market_errors.v1.${service_vendors}.requester.splits.${requester}.${level}.${code}.metrics.hps`](#71d840d615fad73ee1c25d776d93d1ec)
  * [`market-front-unified.market_errors.v1.${service_vendors}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps`](#22b6ddfbf0b042e1faaa593bcd738b9c)
  * [`market-front-unified.market_errors.v1.${service_vendors}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps`](#cf5502fe2b9599658f381fdab7926ca7)
  * [`market-front-unified.market_errors.v1.${service_vendors}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps`](#bea8f1d010a0be9f02eb09f2f0d01f7a)
  * [`market-front-unified.market_errors.v1.${service_vendors}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps`](#788f26625fa810746f352ae4ab567787)
  * [`market-front-unified.market_errors.v1.${service_vendors}.robot.splits.${robot}.${level}.${code}.metrics.hps`](#a496a9c268922f10393707052c46ed04)
  * [`market-front-unified.market_errors.v1.${service_vendors}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps`](#35150ced6a41c9af37497fcec4de8ab8)
  * [`market-front-unified.market_errors.v1.${service_vendors}.total.${level}.${code}.metrics.hps`](#6dd7f72e5273890983cd0ee3a493452a)
  * [`market-front-unified.market_errors.v1.${service_vendors}.type.splits.${type}.${level}.${code}.metrics.hps`](#d332e3428569f335a0a105fa6a7f0e91)

## Metrics

#### <a id='6dd7f72e5273890983cd0ee3a493452a'></a>market-front-unified.market_errors.v1.${service_vendors}.total.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.total.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.total.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8b076453d25f238c44b518a9162de5d0'></a>market-front-unified.market_errors.v1.${service_vendors}.dc.splits.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.dc.splits.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.dc.splits.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7cb818974a43fa4aee62d66ced3ddd08'></a>market-front-unified.market_errors.v1.${service_vendors}.host.splits.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.host.splits.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.host.splits.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d332e3428569f335a0a105fa6a7f0e91'></a>market-front-unified.market_errors.v1.${service_vendors}.type.splits.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.type.splits.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.type.splits.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='71d840d615fad73ee1c25d776d93d1ec'></a>market-front-unified.market_errors.v1.${service_vendors}.requester.splits.${requester}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    requester,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.requester.splits.%24%7Brequester%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.requester.splits.${requester}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        requester,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ec4977f1de99eae94fbb3051749859ad'></a>market-front-unified.market_errors.v1.${service_vendors}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    dc,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.dc.type.splits.%24%7Bdc%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        dc,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ee1853a37a4aa7be659bddf0a23eeb1b'></a>market-front-unified.market_errors.v1.${service_vendors}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20host%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    host,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    host as host,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.host.type.splits.%24%7Bhost%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        host,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        host as host,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='22b6ddfbf0b042e1faaa593bcd738b9c'></a>market-front-unified.market_errors.v1.${service_vendors}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    requester,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.requester.type.splits.%24%7Brequester%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        requester,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='21fd4cd8c6a779b0a585cdeb4cf6b10c'></a>market-front-unified.market_errors.v1.${service_vendors}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    requester,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.requester.dc.splits.%24%7Brequester%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        requester,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9ff303924da56c14fa3db404228a5da4'></a>market-front-unified.market_errors.v1.${service_vendors}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    requester,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.requester.host.splits.%24%7Brequester%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        requester,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a496a9c268922f10393707052c46ed04'></a>market-front-unified.market_errors.v1.${service_vendors}.robot.splits.${robot}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    robot,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.robot.splits.%24%7Brobot%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.robot.splits.${robot}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        robot,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='35150ced6a41c9af37497fcec4de8ab8'></a>market-front-unified.market_errors.v1.${service_vendors}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    robot,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.robot.type.splits.%24%7Brobot%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        robot,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='cf5502fe2b9599658f381fdab7926ca7'></a>market-front-unified.market_errors.v1.${service_vendors}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    robot,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.robot.dc.splits.%24%7Brobot%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        robot,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bea8f1d010a0be9f02eb09f2f0d01f7a'></a>market-front-unified.market_errors.v1.${service_vendors}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    robot,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.robot.host.splits.%24%7Brobot%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        robot,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4b14192f33225b1edb4cc3b9cbe0c87b'></a>market-front-unified.market_errors.v1.${service_vendors}.page.splits.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.page.splits.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.page.splits.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7c2cbf87d47bb60d54cfb050e2dcb205'></a>market-front-unified.market_errors.v1.${service_vendors}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    dc,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.dc.page.splits.%24%7Bdc%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        dc,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d5d00f33ebf7b94cedbfb973810e8cb3'></a>market-front-unified.market_errors.v1.${service_vendors}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20host%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    host,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    host as host,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.host.page.splits.%24%7Bhost%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        host,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        host as host,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='06501fa7f15116cb2ae0b3ce1e4349ca'></a>market-front-unified.market_errors.v1.${service_vendors}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    requester,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.requester.page.splits.%24%7Brequester%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        requester,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='be04bd2ad8cad31b2449621c6e9aa017'></a>market-front-unified.market_errors.v1.${service_vendors}.region.splits.${region}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20region%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    region,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.region.splits.%24%7Bregion%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.region.splits.${region}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        region,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='af546798dc6840c8cf8f67c785831842'></a>market-front-unified.market_errors.v1.${service_vendors}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20region%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    region,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.region.type.splits.%24%7Bregion%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        region,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='477408b9b2152fe5026b560a0d85eb3b'></a>market-front-unified.market_errors.v1.${service_vendors}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20region%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    region,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.region.dc.splits.%24%7Bregion%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        region,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f0a7281165c231b41df2149913ed55ce'></a>market-front-unified.market_errors.v1.${service_vendors}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20region%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    region,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.region.host.splits.%24%7Bregion%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        region,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='788f26625fa810746f352ae4ab567787'></a>market-front-unified.market_errors.v1.${service_vendors}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20''%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    robot,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.robot.page.splits.%24%7Brobot%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20''%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        robot,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='00f858aa5dd97615cb32c24214fc5695'></a>market-front-unified.market_errors.v1.${service_vendors}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_vendors%2C%0A%20%20%20%20region%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20region%20!%3D%20''%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_vendors,
    region,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_vendors%7D.region.page.splits.%24%7Bregion%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_vendors%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_vendors%20!%3D%20'undefined_service'%20and%20region%20!%3D%20''%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_vendors'%5D%2C%20%5B'vendors_desktop'%5D%2C%20'undefined_service'%20)%20as%20service_vendors%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_vendors}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_vendors,
        region,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors,
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
    SELECT 'market-front-unified.market_errors.v1.${service_vendors}.total.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.dc.splits.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.host.splits.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.type.splits.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.requester.splits.${requester}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, requester, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, dc, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, host, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, host as host, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, requester, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, requester, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, requester, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.robot.splits.${robot}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, robot, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, robot, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, robot, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, robot, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.page.splits.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, dc, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, host, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, host as host, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, requester, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.region.splits.${region}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, region, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, region, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_errors.v1.${service_vendors}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, region, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, region, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, robot, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and robot != '' and page != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_vendors}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_vendors, region, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_vendors != 'undefined_service' and region != '' and page != '') GROUP BY metric_ts, transform(service, ['market_front_vendors'], ['vendors_desktop'], 'undefined_service' ) as service_vendors, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

