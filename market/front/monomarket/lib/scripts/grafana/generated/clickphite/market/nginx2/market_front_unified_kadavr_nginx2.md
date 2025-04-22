# market/nginx2/market_front_unified_kadavr_nginx2
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `nginx2`

## Splits

```json
{
    "service_kadavr": "multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' )",
    "code": "arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)])",
    "buckets_ttlb": "if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms))))",
    "buckets_req_time": "if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms))))",
    "buckets_bytes_send": "if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent))))",
    "dc": "multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' )",
    "host": "host",
    "robot": "replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\\\)|MSRBOT \\\\(http://research\\\\.microsoft\\\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\\\.com|Refer\\\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '')"
}
```

## Filters

```json
[
    "url != '/ping' and service_kadavr != 'undefined_service'",
    "url != '/ping' and service_kadavr != 'undefined_service' and robot != ''"
]
```

## Resulting metrics

  * [`market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}`](#b40aa05d1ae1a4d0c530acdb3b8380e5)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.bytes_send.quantiles`](#416fa89e6efbf2697646a93f6d5eda61)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.req_time.buckets.${buckets_req_time}`](#63c81de9a53a9449f02d7bb42e36eac1)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.req_time.quantiles`](#47fc08fd93dd8d3ef917f694de57abf5)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.rps`](#919665b7de45eb668d0fd1055f39b731)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.ttlb.buckets.${buckets_ttlb}`](#dfaffb48d89cae8ed63186c8d241fbf8)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.ttlb.quantiles`](#c38732bf9a18092725e040f0e60a997c)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}`](#f602750e3066d50e9ab68c8eab1cf600)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.bytes_send.quantiles`](#2bdf5f69e87ead9f17f5d0b750193982)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.req_time.buckets.${buckets_req_time}`](#3ec276581042f260d70e6a34718e90be)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.req_time.quantiles`](#b0730f01da5a3962b4a003241892e4f3)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.rps`](#0c4ebbea2435acb87f1288152a634a47)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.ttlb.buckets.${buckets_ttlb}`](#8432269c52c92be3aa9444b3792a4e73)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.ttlb.quantiles`](#b729f8b388e361f16773c505e429e964)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.bytes_send.quantiles`](#be781275bec5d96533791b44d78b05d2)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.req_time.quantiles`](#bc3c2aa8c0dfdfb0311ea67ba71e12fb)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.rps`](#a0bd889b29ec8f41cc243ac3bd0fb0ea)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.ttlb.quantiles`](#18c23d6e0314f0db651f92976d694bfb)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.bytes_send.quantiles`](#a5eb2e818ed82c67f6f7d9a4444acdb0)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.req_time.quantiles`](#77ba494ea7b2a8b09b4b691d955160c6)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.rps`](#bcf5eaaa5f6f0bd3832061b4c822282d)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.ttlb.quantiles`](#62b6a4527824b4f8b582a9e10282152f)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}`](#0fd5525c85b78991091d84d734e4b80e)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.bytes_send.quantiles`](#d37a9bac5f9e0d1248db871270210d80)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.req_time.buckets.${buckets_req_time}`](#5a5efdde61dd54ee66884d5c8da07504)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.req_time.quantiles`](#2f7b24f96286d899dde62c6078966dd4)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.rps`](#830db1ac93f0a7a217ad77abad2de9a0)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.ttlb.buckets.${buckets_ttlb}`](#faba5e5c6ae7c97ea0729d4ed976ac9b)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.ttlb.quantiles`](#61e43b2ae98f51ab98a39d6e6fbc3e81)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}`](#5067f6f915f7993097c267e8305f5b22)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.bytes_send.quantiles`](#aecc45fe66c0fda6f7fe1aaac5020a15)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.req_time.buckets.${buckets_req_time}`](#7f93da8834178450623517fbe02ec8da)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.req_time.quantiles`](#69cb8f99485776d1923f4c2d9d385986)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.rps`](#71c1a0e3d030b599e2a17cf7fe5e1232)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.ttlb.buckets.${buckets_ttlb}`](#5495df4455e151d2a2a07cb590748c5c)
  * [`market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.ttlb.quantiles`](#2d4f86e98a7b1cb9dc4411c487d47972)

## Metrics

#### <a id='71c1a0e3d030b599e2a17cf7fe5e1232'></a>market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.total.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5495df4455e151d2a2a07cb590748c5c'></a>market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.ttlb.buckets.${buckets_ttlb}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_ttlb%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(resptime_ms)%20%3C%20128%2C%20'less_128'%2C%20if(roundToExp2(resptime_ms)%20%3E%2016384%2C%20'more_16384'%2C%20toString(roundToExp2(resptime_ms))))%20as%20buckets_ttlb%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    code,
    buckets_ttlb

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.total.%24%7Bcode%7D.metrics.ttlb.buckets.%24%7Bbuckets_ttlb%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_ttlb%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(resptime_ms)%20%3C%20128%2C%20'less_128'%2C%20if(roundToExp2(resptime_ms)%20%3E%2016384%2C%20'more_16384'%2C%20toString(roundToExp2(resptime_ms))))%20as%20buckets_ttlb%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.ttlb.buckets.${buckets_ttlb}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        code,
        buckets_ttlb
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7f93da8834178450623517fbe02ec8da'></a>market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.req_time.buckets.${buckets_req_time}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_req_time%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(client_reqtime_ms)%20%3C%2064%2C%20'less_64'%2C%20if(roundToExp2(client_reqtime_ms)%20%3E%204096%2C%20'more_4096'%2C%20toString(roundToExp2(client_reqtime_ms))))%20as%20buckets_req_time%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    code,
    buckets_req_time

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.total.%24%7Bcode%7D.metrics.req_time.buckets.%24%7Bbuckets_req_time%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_req_time%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(client_reqtime_ms)%20%3C%2064%2C%20'less_64'%2C%20if(roundToExp2(client_reqtime_ms)%20%3E%204096%2C%20'more_4096'%2C%20toString(roundToExp2(client_reqtime_ms))))%20as%20buckets_req_time%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.req_time.buckets.${buckets_req_time}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        code,
        buckets_req_time
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5067f6f915f7993097c267e8305f5b22'></a>market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_bytes_send%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(bytes_sent)%20%3C%201024%2C%20'less_1024'%2C%20if(roundToExp2(bytes_sent)%20%3E%2065536%2C%20'more_65536'%2C%20toString(roundToExp2(bytes_sent))))%20as%20buckets_bytes_send%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    code,
    buckets_bytes_send

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.total.%24%7Bcode%7D.metrics.bytes_send.buckets.%24%7Bbuckets_bytes_send%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_bytes_send%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(bytes_sent)%20%3C%201024%2C%20'less_1024'%2C%20if(roundToExp2(bytes_sent)%20%3E%2065536%2C%20'more_65536'%2C%20toString(roundToExp2(bytes_sent))))%20as%20buckets_bytes_send%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        code,
        buckets_bytes_send
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='919665b7de45eb668d0fd1055f39b731'></a>market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    dc,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.dc.splits.%24%7Bdc%7D.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        dc,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='dfaffb48d89cae8ed63186c8d241fbf8'></a>market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.ttlb.buckets.${buckets_ttlb}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_ttlb%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(resptime_ms)%20%3C%20128%2C%20'less_128'%2C%20if(roundToExp2(resptime_ms)%20%3E%2016384%2C%20'more_16384'%2C%20toString(roundToExp2(resptime_ms))))%20as%20buckets_ttlb%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    dc,
    code,
    buckets_ttlb

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.dc.splits.%24%7Bdc%7D.%24%7Bcode%7D.metrics.ttlb.buckets.%24%7Bbuckets_ttlb%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_ttlb%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(resptime_ms)%20%3C%20128%2C%20'less_128'%2C%20if(roundToExp2(resptime_ms)%20%3E%2016384%2C%20'more_16384'%2C%20toString(roundToExp2(resptime_ms))))%20as%20buckets_ttlb%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.ttlb.buckets.${buckets_ttlb}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        dc,
        code,
        buckets_ttlb
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='63c81de9a53a9449f02d7bb42e36eac1'></a>market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.req_time.buckets.${buckets_req_time}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_req_time%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(client_reqtime_ms)%20%3C%2064%2C%20'less_64'%2C%20if(roundToExp2(client_reqtime_ms)%20%3E%204096%2C%20'more_4096'%2C%20toString(roundToExp2(client_reqtime_ms))))%20as%20buckets_req_time%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    dc,
    code,
    buckets_req_time

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.dc.splits.%24%7Bdc%7D.%24%7Bcode%7D.metrics.req_time.buckets.%24%7Bbuckets_req_time%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_req_time%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(client_reqtime_ms)%20%3C%2064%2C%20'less_64'%2C%20if(roundToExp2(client_reqtime_ms)%20%3E%204096%2C%20'more_4096'%2C%20toString(roundToExp2(client_reqtime_ms))))%20as%20buckets_req_time%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.req_time.buckets.${buckets_req_time}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        dc,
        code,
        buckets_req_time
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b40aa05d1ae1a4d0c530acdb3b8380e5'></a>market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_bytes_send%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(bytes_sent)%20%3C%201024%2C%20'less_1024'%2C%20if(roundToExp2(bytes_sent)%20%3E%2065536%2C%20'more_65536'%2C%20toString(roundToExp2(bytes_sent))))%20as%20buckets_bytes_send%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    dc,
    code,
    buckets_bytes_send

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.dc.splits.%24%7Bdc%7D.%24%7Bcode%7D.metrics.bytes_send.buckets.%24%7Bbuckets_bytes_send%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_bytes_send%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(bytes_sent)%20%3C%201024%2C%20'less_1024'%2C%20if(roundToExp2(bytes_sent)%20%3E%2065536%2C%20'more_65536'%2C%20toString(roundToExp2(bytes_sent))))%20as%20buckets_bytes_send%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        dc,
        code,
        buckets_bytes_send
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0c4ebbea2435acb87f1288152a634a47'></a>market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20host%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    host,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    host as host,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.host.splits.%24%7Bhost%7D.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        host,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        host as host,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8432269c52c92be3aa9444b3792a4e73'></a>market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.ttlb.buckets.${buckets_ttlb}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20host%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_ttlb%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(resptime_ms)%20%3C%20128%2C%20'less_128'%2C%20if(roundToExp2(resptime_ms)%20%3E%2016384%2C%20'more_16384'%2C%20toString(roundToExp2(resptime_ms))))%20as%20buckets_ttlb%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    host,
    code,
    buckets_ttlb

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    host as host,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.host.splits.%24%7Bhost%7D.%24%7Bcode%7D.metrics.ttlb.buckets.%24%7Bbuckets_ttlb%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_ttlb%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(resptime_ms)%20%3C%20128%2C%20'less_128'%2C%20if(roundToExp2(resptime_ms)%20%3E%2016384%2C%20'more_16384'%2C%20toString(roundToExp2(resptime_ms))))%20as%20buckets_ttlb%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.ttlb.buckets.${buckets_ttlb}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        host,
        code,
        buckets_ttlb
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        host as host,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3ec276581042f260d70e6a34718e90be'></a>market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.req_time.buckets.${buckets_req_time}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20host%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_req_time%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(client_reqtime_ms)%20%3C%2064%2C%20'less_64'%2C%20if(roundToExp2(client_reqtime_ms)%20%3E%204096%2C%20'more_4096'%2C%20toString(roundToExp2(client_reqtime_ms))))%20as%20buckets_req_time%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    host,
    code,
    buckets_req_time

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    host as host,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.host.splits.%24%7Bhost%7D.%24%7Bcode%7D.metrics.req_time.buckets.%24%7Bbuckets_req_time%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_req_time%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(client_reqtime_ms)%20%3C%2064%2C%20'less_64'%2C%20if(roundToExp2(client_reqtime_ms)%20%3E%204096%2C%20'more_4096'%2C%20toString(roundToExp2(client_reqtime_ms))))%20as%20buckets_req_time%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.req_time.buckets.${buckets_req_time}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        host,
        code,
        buckets_req_time
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        host as host,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f602750e3066d50e9ab68c8eab1cf600'></a>market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20host%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_bytes_send%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(bytes_sent)%20%3C%201024%2C%20'less_1024'%2C%20if(roundToExp2(bytes_sent)%20%3E%2065536%2C%20'more_65536'%2C%20toString(roundToExp2(bytes_sent))))%20as%20buckets_bytes_send%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    host,
    code,
    buckets_bytes_send

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    host as host,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.host.splits.%24%7Bhost%7D.%24%7Bcode%7D.metrics.bytes_send.buckets.%24%7Bbuckets_bytes_send%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_bytes_send%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(bytes_sent)%20%3C%201024%2C%20'less_1024'%2C%20if(roundToExp2(bytes_sent)%20%3E%2065536%2C%20'more_65536'%2C%20toString(roundToExp2(bytes_sent))))%20as%20buckets_bytes_send%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        host,
        code,
        buckets_bytes_send
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        host as host,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='830db1ac93f0a7a217ad77abad2de9a0'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    robot,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.splits.%24%7Brobot%7D.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        robot,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='faba5e5c6ae7c97ea0729d4ed976ac9b'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.ttlb.buckets.${buckets_ttlb}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_ttlb%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(resptime_ms)%20%3C%20128%2C%20'less_128'%2C%20if(roundToExp2(resptime_ms)%20%3E%2016384%2C%20'more_16384'%2C%20toString(roundToExp2(resptime_ms))))%20as%20buckets_ttlb%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    robot,
    code,
    buckets_ttlb

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.splits.%24%7Brobot%7D.%24%7Bcode%7D.metrics.ttlb.buckets.%24%7Bbuckets_ttlb%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_ttlb%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(resptime_ms)%20%3C%20128%2C%20'less_128'%2C%20if(roundToExp2(resptime_ms)%20%3E%2016384%2C%20'more_16384'%2C%20toString(roundToExp2(resptime_ms))))%20as%20buckets_ttlb%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.ttlb.buckets.${buckets_ttlb}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        robot,
        code,
        buckets_ttlb
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5a5efdde61dd54ee66884d5c8da07504'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.req_time.buckets.${buckets_req_time}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_req_time%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(client_reqtime_ms)%20%3C%2064%2C%20'less_64'%2C%20if(roundToExp2(client_reqtime_ms)%20%3E%204096%2C%20'more_4096'%2C%20toString(roundToExp2(client_reqtime_ms))))%20as%20buckets_req_time%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    robot,
    code,
    buckets_req_time

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.splits.%24%7Brobot%7D.%24%7Bcode%7D.metrics.req_time.buckets.%24%7Bbuckets_req_time%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_req_time%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(client_reqtime_ms)%20%3C%2064%2C%20'less_64'%2C%20if(roundToExp2(client_reqtime_ms)%20%3E%204096%2C%20'more_4096'%2C%20toString(roundToExp2(client_reqtime_ms))))%20as%20buckets_req_time%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.req_time.buckets.${buckets_req_time}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        robot,
        code,
        buckets_req_time
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0fd5525c85b78991091d84d734e4b80e'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20code%2C%0A%20%20%20%20buckets_bytes_send%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20if(roundToExp2(bytes_sent)%20%3C%201024%2C%20'less_1024'%2C%20if(roundToExp2(bytes_sent)%20%3E%2065536%2C%20'more_65536'%2C%20toString(roundToExp2(bytes_sent))))%20as%20buckets_bytes_send%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    robot,
    code,
    buckets_bytes_send

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
    if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.splits.%24%7Brobot%7D.%24%7Bcode%7D.metrics.bytes_send.buckets.%24%7Bbuckets_bytes_send%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20code%2C%0A%20%20%20%20%20%20%20%20buckets_bytes_send%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(bytes_sent)%20%3C%201024%2C%20'less_1024'%2C%20if(roundToExp2(bytes_sent)%20%3E%2065536%2C%20'more_65536'%2C%20toString(roundToExp2(bytes_sent))))%20as%20buckets_bytes_send%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        robot,
        code,
        buckets_bytes_send
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code,
        if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a0bd889b29ec8f41cc243ac3bd0fb0ea'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    robot,
    dc,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.dc.splits.%24%7Brobot%7D.%24%7Bdc%7D.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        robot,
        dc,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bcf5eaaa5f6f0bd3832061b4c822282d'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20host%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_kadavr,
    robot,
    host,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    host as host,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.host.splits.%24%7Brobot%7D.%24%7Bhost%7D.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_kadavr,
        robot,
        host,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        host as host,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2d4f86e98a7b1cb9dc4411c487d47972'></a>market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
    service_kadavr,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.total.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
        service_kadavr,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c38732bf9a18092725e040f0e60a997c'></a>market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
    service_kadavr,
    dc,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.dc.splits.%24%7Bdc%7D.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
        service_kadavr,
        dc,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b729f8b388e361f16773c505e429e964'></a>market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20host%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
    service_kadavr,
    host,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    host as host,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.host.splits.%24%7Bhost%7D.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
        service_kadavr,
        host,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        host as host,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='61e43b2ae98f51ab98a39d6e6fbc3e81'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
    service_kadavr,
    robot,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.splits.%24%7Brobot%7D.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
        service_kadavr,
        robot,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='18c23d6e0314f0db651f92976d694bfb'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
    service_kadavr,
    robot,
    dc,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.dc.splits.%24%7Brobot%7D.%24%7Bdc%7D.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
        service_kadavr,
        robot,
        dc,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='62b6a4527824b4f8b582a9e10282152f'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20host%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
    service_kadavr,
    robot,
    host,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    host as host,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.host.splits.%24%7Brobot%7D.%24%7Bhost%7D.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(resptime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
        service_kadavr,
        robot,
        host,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        host as host,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='69cb8f99485776d1923f4c2d9d385986'></a>market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.req_time.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
    service_kadavr,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.total.%24%7Bcode%7D.metrics.req_time.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.req_time.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
        service_kadavr,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='47fc08fd93dd8d3ef917f694de57abf5'></a>market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.req_time.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
    service_kadavr,
    dc,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.dc.splits.%24%7Bdc%7D.%24%7Bcode%7D.metrics.req_time.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.req_time.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
        service_kadavr,
        dc,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b0730f01da5a3962b4a003241892e4f3'></a>market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.req_time.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20host%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
    service_kadavr,
    host,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    host as host,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.host.splits.%24%7Bhost%7D.%24%7Bcode%7D.metrics.req_time.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.req_time.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
        service_kadavr,
        host,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        host as host,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2f7b24f96286d899dde62c6078966dd4'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.req_time.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
    service_kadavr,
    robot,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.splits.%24%7Brobot%7D.%24%7Bcode%7D.metrics.req_time.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.req_time.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
        service_kadavr,
        robot,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bc3c2aa8c0dfdfb0311ea67ba71e12fb'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.req_time.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
    service_kadavr,
    robot,
    dc,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.dc.splits.%24%7Brobot%7D.%24%7Bdc%7D.%24%7Bcode%7D.metrics.req_time.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.req_time.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
        service_kadavr,
        robot,
        dc,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='77ba494ea7b2a8b09b4b691d955160c6'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.req_time.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20host%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
    service_kadavr,
    robot,
    host,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    host as host,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.host.splits.%24%7Brobot%7D.%24%7Bhost%7D.%24%7Bcode%7D.metrics.req_time.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(client_reqtime_ms%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.req_time.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
        service_kadavr,
        robot,
        host,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        host as host,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='aecc45fe66c0fda6f7fe1aaac5020a15'></a>market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
    service_kadavr,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.total.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
        service_kadavr,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='416fa89e6efbf2697646a93f6d5eda61'></a>market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
    service_kadavr,
    dc,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.dc.splits.%24%7Bdc%7D.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
        service_kadavr,
        dc,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2bdf5f69e87ead9f17f5d0b750193982'></a>market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20host%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
    service_kadavr,
    host,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    host as host,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.host.splits.%24%7Bhost%7D.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service') as value_0,
        service_kadavr,
        host,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        host as host,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d37a9bac5f9e0d1248db871270210d80'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
    service_kadavr,
    robot,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.splits.%24%7Brobot%7D.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
        service_kadavr,
        robot,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='be781275bec5d96533791b44d78b05d2'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
    service_kadavr,
    robot,
    dc,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.dc.splits.%24%7Brobot%7D.%24%7Bdc%7D.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
        service_kadavr,
        robot,
        dc,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a5eb2e818ed82c67f6f7d9a4444acdb0'></a>market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20service_kadavr%2C%0A%20%20%20%20robot%2C%0A%20%20%20%20host%2C%0A%20%20%20%20code%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
    service_kadavr,
    robot,
    host,
    code

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')

GROUP BY metric_ts,
    multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
    replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
    host as host,
    arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.nginx2.v2.%24%7Bservice_kadavr%7D.robot.host.splits.%24%7Brobot%7D.%24%7Bhost%7D.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(bytes_sent%2Curl%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20robot%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(url%20!%3D%20'%2Fping'%20and%20service_kadavr%20!%3D%20'undefined_service'%20and%20robot%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('kadavr.vs.market.yandex.net'%2C'kadavr2.vs.market.yandex.net'%2C'kadavr3.vs.market.yandex.net'%2C'kadavr4.vs.market.yandex.net')%2C%20'kadavr'%20%2C%20'undefined_service'%20)%20as%20service_kadavr%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20robot%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-code'%2C%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%2C%20toString(http_code)%5D)%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0,
        service_kadavr,
        robot,
        host,
        code
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr,
        replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot,
        host as host,
        arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```


## Overall Diagnostics

### Portion #1

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.ttlb.buckets.${buckets_ttlb}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, code, buckets_ttlb FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.req_time.buckets.${buckets_req_time}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, code, buckets_req_time FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, code, buckets_bytes_send FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, dc, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.ttlb.buckets.${buckets_ttlb}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, dc, code, buckets_ttlb FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.req_time.buckets.${buckets_req_time}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, dc, code, buckets_req_time FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, dc, code, buckets_bytes_send FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, host, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, host as host, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.ttlb.buckets.${buckets_ttlb}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, host, code, buckets_ttlb FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, host as host, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.req_time.buckets.${buckets_req_time}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, host, code, buckets_req_time FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, host as host, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, host, code, buckets_bytes_send FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, host as host, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, robot, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.ttlb.buckets.${buckets_ttlb}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, robot, code, buckets_ttlb FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(resptime_ms) < 128, 'less_128', if(roundToExp2(resptime_ms) > 16384, 'more_16384', toString(roundToExp2(resptime_ms)))) as buckets_ttlb ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.req_time.buckets.${buckets_req_time}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, robot, code, buckets_req_time FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(client_reqtime_ms) < 64, 'less_64', if(roundToExp2(client_reqtime_ms) > 4096, 'more_4096', toString(roundToExp2(client_reqtime_ms)))) as buckets_req_time ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.bytes_send.buckets.${buckets_bytes_send}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, robot, code, buckets_bytes_send FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code, if(roundToExp2(bytes_sent) < 1024, 'less_1024', if(roundToExp2(bytes_sent) > 65536, 'more_65536', toString(roundToExp2(bytes_sent)))) as buckets_bytes_send ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, robot, dc, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_kadavr, robot, host, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, host as host, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0, service_kadavr, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0, service_kadavr, dc, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0, service_kadavr, host, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, host as host, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0, service_kadavr, robot, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0, service_kadavr, robot, dc, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(resptime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0, service_kadavr, robot, host, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, host as host, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.req_time.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0, service_kadavr, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.req_time.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0, service_kadavr, dc, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.req_time.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service') as value_0, service_kadavr, host, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, host as host, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.req_time.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0, service_kadavr, robot, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.req_time.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0, service_kadavr, robot, dc, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.req_time.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(client_reqtime_ms,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0, service_kadavr, robot, host, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, host as host, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.total.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service') as value_0, service_kadavr, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.dc.splits.${dc}.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service') as value_0, service_kadavr, dc, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.host.splits.${host}.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service') as value_0, service_kadavr, host, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, host as host, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.splits.${robot}.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0, service_kadavr, robot, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.dc.splits.${robot}.${dc}.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0, service_kadavr, robot, dc, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.nginx2.v2.${service_kadavr}.robot.host.splits.${robot}.${host}.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(bytes_sent,url != '/ping' and service_kadavr != 'undefined_service' and robot != '') as value_0, service_kadavr, robot, host, code FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (url != '/ping' and service_kadavr != 'undefined_service' and robot != '') GROUP BY metric_ts, multiIf( vhost in ('kadavr.vs.market.yandex.net','kadavr2.vs.market.yandex.net','kadavr3.vs.market.yandex.net','kadavr4.vs.market.yandex.net'), 'kadavr' , 'undefined_service' ) as service_kadavr, replaceRegexpAll(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/'),'[^a-zA-Z0-9]', '') as robot, host as host, arrayJoin(['any-code', concat(substring(toString(http_code),1,1),'xx'), toString(http_code)]) as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

