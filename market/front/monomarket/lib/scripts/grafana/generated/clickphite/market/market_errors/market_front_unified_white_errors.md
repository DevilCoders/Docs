# market/market_errors/market_front_unified_white_errors
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `market_errors`

## Splits

```json
{
    "service_white": "transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' )",
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
    "environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service'",
    "environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '' and page != ''",
    "environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '' and page != ''"
]
```

## Resulting metrics

  * [`market-front-unified.market_errors.v1.${service_white}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps`](#47963b90a44a108772564f47031c4043)
  * [`market-front-unified.market_errors.v1.${service_white}.dc.splits.${dc}.${level}.${code}.metrics.hps`](#232fb1c7ba6fa930a841046d7bee93a7)
  * [`market-front-unified.market_errors.v1.${service_white}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps`](#559b952e2888d469b4aa93c22bcbc594)
  * [`market-front-unified.market_errors.v1.${service_white}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps`](#0e684ece8c14fb205fc1cbf2d31a954b)
  * [`market-front-unified.market_errors.v1.${service_white}.host.splits.${host}.${level}.${code}.metrics.hps`](#17ec1b5f5f5927e6fac740ff7596d0aa)
  * [`market-front-unified.market_errors.v1.${service_white}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps`](#110b014b5df6d204d1c3afdaf0b95ca3)
  * [`market-front-unified.market_errors.v1.${service_white}.page.splits.${page}.${level}.${code}.metrics.hps`](#4c0d1572ec2283810e6b735e9f0d01c8)
  * [`market-front-unified.market_errors.v1.${service_white}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps`](#9c8c2d17a7f37f15a0c4e83d9c04a5c3)
  * [`market-front-unified.market_errors.v1.${service_white}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps`](#1a2730b6b57b6e58da6d4097425171c0)
  * [`market-front-unified.market_errors.v1.${service_white}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps`](#150fe47301509b5a0b9b73c81b4ed6e3)
  * [`market-front-unified.market_errors.v1.${service_white}.region.splits.${region}.${level}.${code}.metrics.hps`](#52fcdc07c1b6e78fe5077b617c43b825)
  * [`market-front-unified.market_errors.v1.${service_white}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps`](#a1607e4e66a2e55267892ff2be32e572)
  * [`market-front-unified.market_errors.v1.${service_white}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps`](#842cd928289464a5c791be3d134a04b0)
  * [`market-front-unified.market_errors.v1.${service_white}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps`](#a0196d17f8bdbf37b525da06e9817590)
  * [`market-front-unified.market_errors.v1.${service_white}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps`](#ce1290b38ee858b8d7ee97d373a9365e)
  * [`market-front-unified.market_errors.v1.${service_white}.requester.splits.${requester}.${level}.${code}.metrics.hps`](#05c8f4a0ac0434626e12f5f90c0eb8e6)
  * [`market-front-unified.market_errors.v1.${service_white}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps`](#06cf98f34e0ab005a94f466c6dc32413)
  * [`market-front-unified.market_errors.v1.${service_white}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps`](#75df8b4b1f60e6388aebcfb32522c0b8)
  * [`market-front-unified.market_errors.v1.${service_white}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps`](#acd3d4121edbe74d15cadbfb0bc68e74)
  * [`market-front-unified.market_errors.v1.${service_white}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps`](#402bf9573f267ed902de8491f4f3a239)
  * [`market-front-unified.market_errors.v1.${service_white}.robot.splits.${robot}.${level}.${code}.metrics.hps`](#b4c57a885abb9773c308935b6368a1b3)
  * [`market-front-unified.market_errors.v1.${service_white}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps`](#6012d75942f3a058d88d79d8b8e335b1)
  * [`market-front-unified.market_errors.v1.${service_white}.total.${level}.${code}.metrics.hps`](#68deecd709d37296dd2b214c350bd4f3)
  * [`market-front-unified.market_errors.v1.${service_white}.type.splits.${type}.${level}.${code}.metrics.hps`](#7c0f2d165e8f02b8fced8e7f9c48e329)

## Metrics

#### <a id='68deecd709d37296dd2b214c350bd4f3'></a>market-front-unified.market_errors.v1.${service_white}.total.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.total.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.total.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='232fb1c7ba6fa930a841046d7bee93a7'></a>market-front-unified.market_errors.v1.${service_white}.dc.splits.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.dc.splits.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.dc.splits.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='17ec1b5f5f5927e6fac740ff7596d0aa'></a>market-front-unified.market_errors.v1.${service_white}.host.splits.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.host.splits.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.host.splits.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7c0f2d165e8f02b8fced8e7f9c48e329'></a>market-front-unified.market_errors.v1.${service_white}.type.splits.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.type.splits.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.type.splits.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='05c8f4a0ac0434626e12f5f90c0eb8e6'></a>market-front-unified.market_errors.v1.${service_white}.requester.splits.${requester}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.requester.splits.${requester}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='559b952e2888d469b4aa93c22bcbc594'></a>market-front-unified.market_errors.v1.${service_white}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    dc,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.dc.type.splits.%24%7Bdc%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        dc,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='110b014b5df6d204d1c3afdaf0b95ca3'></a>market-front-unified.market_errors.v1.${service_white}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20host%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    host,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    host as host,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.host.type.splits.%24%7Bhost%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        host,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        host as host,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='06cf98f34e0ab005a94f466c6dc32413'></a>market-front-unified.market_errors.v1.${service_white}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.requester.type.splits.%24%7Brequester%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='842cd928289464a5c791be3d134a04b0'></a>market-front-unified.market_errors.v1.${service_white}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.requester.dc.splits.%24%7Brequester%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a0196d17f8bdbf37b525da06e9817590'></a>market-front-unified.market_errors.v1.${service_white}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.requester.host.splits.%24%7Brequester%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b4c57a885abb9773c308935b6368a1b3'></a>market-front-unified.market_errors.v1.${service_white}.robot.splits.${robot}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robot,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.robot.splits.%24%7Brobot%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.robot.splits.${robot}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robot,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6012d75942f3a058d88d79d8b8e335b1'></a>market-front-unified.market_errors.v1.${service_white}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robot,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.robot.type.splits.%24%7Brobot%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robot,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='75df8b4b1f60e6388aebcfb32522c0b8'></a>market-front-unified.market_errors.v1.${service_white}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robot,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.robot.dc.splits.%24%7Brobot%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robot,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='acd3d4121edbe74d15cadbfb0bc68e74'></a>market-front-unified.market_errors.v1.${service_white}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robot,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.robot.host.splits.%24%7Brobot%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robot,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4c0d1572ec2283810e6b735e9f0d01c8'></a>market-front-unified.market_errors.v1.${service_white}.page.splits.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.page.splits.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.page.splits.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='47963b90a44a108772564f47031c4043'></a>market-front-unified.market_errors.v1.${service_white}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    dc,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.dc.page.splits.%24%7Bdc%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        dc,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0e684ece8c14fb205fc1cbf2d31a954b'></a>market-front-unified.market_errors.v1.${service_white}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20host%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    host,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    host as host,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.host.page.splits.%24%7Bhost%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        host,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        host as host,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ce1290b38ee858b8d7ee97d373a9365e'></a>market-front-unified.market_errors.v1.${service_white}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.requester.page.splits.%24%7Brequester%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20multiIf(%20indexOf(extra_keys%2C%20'user-agent')%20%3D%200%2C%20'unknown'%2C%20extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20extra_values%5BindexOf(extra_keys%2C%20'user-agent')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='52fcdc07c1b6e78fe5077b617c43b825'></a>market-front-unified.market_errors.v1.${service_white}.region.splits.${region}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20region%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    region,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.region.splits.%24%7Bregion%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.region.splits.${region}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        region,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a1607e4e66a2e55267892ff2be32e572'></a>market-front-unified.market_errors.v1.${service_white}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20region%2C%0A%20%20%20%20type%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    region,
    type,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.region.type.splits.%24%7Bregion%7D.%24%7Btype%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20type%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(tags%5B1%5D%2C%20'')%2C%20'UNKNOWN')%20as%20type%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        region,
        type,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9c8c2d17a7f37f15a0c4e83d9c04a5c3'></a>market-front-unified.market_errors.v1.${service_white}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20region%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    region,
    dc,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.region.dc.splits.%24%7Bregion%7D.%24%7Bdc%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        region,
        dc,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1a2730b6b57b6e58da6d4097425171c0'></a>market-front-unified.market_errors.v1.${service_white}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20region%2C%0A%20%20%20%20host%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    region,
    host,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    host as host,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.region.host.splits.%24%7Bregion%7D.%24%7Bhost%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        region,
        host,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
        host as host,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='402bf9573f267ed902de8491f4f3a239'></a>market-front-unified.market_errors.v1.${service_white}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20''%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robot,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.robot.page.splits.%24%7Brobot%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20''%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(decodeURLComponent(extra_values%5BindexOf(extra_keys%2C%20'user-agent')%20as%20idx%5D)%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robot,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
        replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
        arrayJoin([level, 'any-level']) as level,
        replaceAll(code, '.', '_') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='150fe47301509b5a0b9b73c81b4ed6e3'></a>market-front-unified.market_errors.v1.${service_white}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20region%2C%0A%20%20%20%20page%2C%0A%20%20%20%20level%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_errors%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20region%20!%3D%20''%20and%20page%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    region,
    page,
    level,
    code

FROM market.market_errors

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '' and page != '')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region,
    replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page,
    arrayJoin([level, 'any-level']) as level,
    replaceAll(code, '.', '_') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_errors.v1.%24%7Bservice_white%7D.region.page.splits.%24%7Bregion%7D.%24%7Bpage%7D.%24%7Blevel%7D.%24%7Bcode%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20level%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_errors%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20platform%20%3D%20'server'%20and%20service_white%20!%3D%20'undefined_service'%20and%20region%20!%3D%20''%20and%20page%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_touch_api'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'white_fapi'%5D%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values%5BindexOf(extra_keys%2C%20'region')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20replaceAll(extra_values%5BindexOf(extra_keys%2C%20'page')%5D%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5Blevel%2C%20'any-level'%5D)%20as%20level%2C%0A%20%20%20%20%20%20%20%20replaceAll(code%2C%20'.'%2C%20'_')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_errors.v1.${service_white}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        region,
        page,
        level,
        code
    
    FROM market.market_errors
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '' and page != '')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white,
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
    SELECT 'market-front-unified.market_errors.v1.${service_white}.total.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.dc.splits.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.host.splits.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.type.splits.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.requester.splits.${requester}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.dc.type.splits.${dc}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, dc, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.host.type.splits.${host}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, host, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, host as host, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.requester.type.splits.${requester}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.requester.dc.splits.${requester}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.requester.host.splits.${requester}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.robot.splits.${robot}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robot, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.robot.type.splits.${robot}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robot, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.robot.dc.splits.${robot}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robot, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.robot.host.splits.${robot}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robot, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.page.splits.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.dc.page.splits.${dc}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, dc, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.host.page.splits.${host}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, host, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, host as host, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.requester.page.splits.${requester}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and page != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, multiIf( indexOf(extra_keys, 'user-agent') = 0, 'unknown', extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', extra_values[indexOf(extra_keys, 'user-agent')] = '', 'anonymous', 'logged-in' ) as requester, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.region.splits.${region}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, region, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.region.type.splits.${region}.${type}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, region, type, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, coalesce(nullIf(tags[1], ''), 'UNKNOWN') as type, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_errors.v1.${service_white}.region.dc.splits.${region}.${dc}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, region, dc, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.region.host.splits.${region}.${host}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, region, host, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, host as host, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.robot.page.splits.${robot}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robot, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and robot != '' and page != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, replaceRegexpAll(extract(decodeURLComponent(extra_values[indexOf(extra_keys, 'user-agent') as idx]),'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_errors.v1.${service_white}.region.page.splits.${region}.${page}.${level}.${code}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, region, page, level, code FROM market.market_errors WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and platform = 'server' and service_white != 'undefined_service' and region != '' and page != '') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_touch_api'], ['white_desktop','white_touch','white_fapi'], 'undefined_service' ) as service_white, replaceAll(regionToName(regionToCountry(toUInt32OrZero(extra_values[indexOf(extra_keys, 'region')])), 'en'), ' ', '_') as region, replaceAll(extra_values[indexOf(extra_keys, 'page')], ':', '_') as page, arrayJoin([level, 'any-level']) as level, replaceAll(code, '.', '_') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

