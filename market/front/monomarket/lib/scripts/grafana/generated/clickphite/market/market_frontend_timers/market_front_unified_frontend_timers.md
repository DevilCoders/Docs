# market/market_frontend_timers/market_front_unified_frontend_timers
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `market_frontend_timers`

## Splits

```json
{
    "service": "transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' )",
    "buckets_tick": "roundToExp2(duration_ms)",
    "buckets_lag": "roundToExp2(duration_ms)",
    "buckets_boredom": "roundToExp2(duration_ms)",
    "buckets_render": "roundToExp2(duration_ms)",
    "page": "arrayJoin(['any-page', replaceAll(page_id, ':', '_')])",
    "widget": "replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '')",
    "buckets_stuffing": "roundToExp2(duration_ms)",
    "buckets_shipping": "roundToExp2(duration_ms)",
    "buckets_rendering": "roundToExp2(duration_ms)",
    "buckets_shaping": "roundToExp2(duration_ms)"
}
```

## Filters

```json
[
    "environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxTickTime'",
    "environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxLag'",
    "environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'boredom' and type = 'total'",
    "environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'render' and type = 'total'",
    "environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing'",
    "environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shipping'",
    "environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-rendering'",
    "environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shaping'"
]
```

## Resulting metrics

  * [`market-front-unified.market_frontend_timers.v1.${service}.nodejs.boredom.buckets.${buckets_boredom}`](#a4d0c18e827c7064510e23fec7f01818)
  * [`market-front-unified.market_frontend_timers.v1.${service}.nodejs.boredom.quantiles`](#3e5374e28813b53dac233b7c42fe1815)
  * [`market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.lag.buckets.${buckets_lag}`](#e819c0a653299bdae5903da6a5226d59)
  * [`market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.lag.quantiles`](#619935c54ad97851590e09e1df0cef16)
  * [`market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.tick.buckets.${buckets_tick}`](#3fa479f5d15ea20bdfdf2f600d89d1b5)
  * [`market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.tick.quantiles`](#009ff1ca87caa6dd47a7ecc78c57dcd8)
  * [`market-front-unified.market_frontend_timers.v1.${service}.nodejs.render.buckets.${buckets_render}`](#9027481d4c256ab782a8578e569be785)
  * [`market-front-unified.market_frontend_timers.v1.${service}.nodejs.render.quantiles`](#46173d9810102cd00eca47b28fd94c7e)
  * [`market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.hps`](#c883627cec4621e4f6278665abfdf8b7)
  * [`market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.rendering.buckets.${buckets_rendering}`](#3ebfcd3c4a5bf6bf74521988187e02ba)
  * [`market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.rendering.quantiles`](#23ed60d8fd3b37b867c81344cd130dde)
  * [`market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shaping.buckets.${buckets_shaping}`](#f52abba6b0994be0c834320612b8ff8b)
  * [`market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shaping.quantiles`](#89959efd281958abf6980c1eba65ecac)
  * [`market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shipping.buckets.${buckets_shipping}`](#8c3b34cbd0d3ddec21530dabc4239895)
  * [`market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shipping.quantiles`](#60cc2dd8704f1b2409b3659b682bf2be)
  * [`market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.stuffing.buckets.${buckets_stuffing}`](#ba58a97f55a43507fa6b274f367c0189)
  * [`market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.stuffing.quantiles`](#da1c5abd4c59fb50f4054e6ed0e9d8b6)

## Metrics

#### <a id='009ff1ca87caa6dd47a7ecc78c57dcd8'></a>market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.tick.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxTickTime')%20as%20value_0%2C%0A%20%20%20%20service%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxTickTime')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxTickTime') as value_0,
    service

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxTickTime')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.nodejs.eventLoop.tick.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxTickTime')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxTickTime')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.tick.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxTickTime') as value_0,
        service
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxTickTime')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='619935c54ad97851590e09e1df0cef16'></a>market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.lag.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxLag')%20as%20value_0%2C%0A%20%20%20%20service%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxLag')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxLag') as value_0,
    service

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxLag')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.nodejs.eventLoop.lag.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxLag')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxLag')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.lag.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxLag') as value_0,
        service
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxLag')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3e5374e28813b53dac233b7c42fe1815'></a>market-front-unified.market_frontend_timers.v1.${service}.nodejs.boredom.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'boredom'%20and%20type%20%3D%20'total')%20as%20value_0%2C%0A%20%20%20%20service%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'boredom'%20and%20type%20%3D%20'total')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'boredom' and type = 'total') as value_0,
    service

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'boredom' and type = 'total')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.nodejs.boredom.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'boredom'%20and%20type%20%3D%20'total')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'boredom'%20and%20type%20%3D%20'total')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.nodejs.boredom.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'boredom' and type = 'total') as value_0,
        service
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'boredom' and type = 'total')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='46173d9810102cd00eca47b28fd94c7e'></a>market-front-unified.market_frontend_timers.v1.${service}.nodejs.render.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'render'%20and%20type%20%3D%20'total')%20as%20value_0%2C%0A%20%20%20%20service%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'render'%20and%20type%20%3D%20'total')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'render' and type = 'total') as value_0,
    service

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'render' and type = 'total')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.nodejs.render.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'render'%20and%20type%20%3D%20'total')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'render'%20and%20type%20%3D%20'total')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.nodejs.render.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'render' and type = 'total') as value_0,
        service
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'render' and type = 'total')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='da1c5abd4c59fb50f4054e6ed0e9d8b6'></a>market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-stuffing')%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-stuffing')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing') as value_0,
    service,
    page,
    widget

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.widgets.%24%7Bpage%7D.%24%7Bwidget%7D.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-stuffing')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-stuffing')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing') as value_0,
        service,
        page,
        widget
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='60cc2dd8704f1b2409b3659b682bf2be'></a>market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shipping.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shipping')%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shipping')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shipping') as value_0,
    service,
    page,
    widget

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shipping')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.widgets.%24%7Bpage%7D.%24%7Bwidget%7D.shipping.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shipping')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shipping')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shipping.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shipping') as value_0,
        service,
        page,
        widget
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shipping')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='23ed60d8fd3b37b867c81344cd130dde'></a>market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.rendering.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-rendering')%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-rendering')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-rendering') as value_0,
    service,
    page,
    widget

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-rendering')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.widgets.%24%7Bpage%7D.%24%7Bwidget%7D.rendering.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-rendering')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-rendering')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.rendering.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-rendering') as value_0,
        service,
        page,
        widget
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-rendering')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='89959efd281958abf6980c1eba65ecac'></a>market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shaping.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shaping')%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shaping')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shaping') as value_0,
    service,
    page,
    widget

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shaping')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.widgets.%24%7Bpage%7D.%24%7Bwidget%7D.shaping.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shaping')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shaping')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shaping.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shaping') as value_0,
        service,
        page,
        widget
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shaping')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3fa479f5d15ea20bdfdf2f600d89d1b5'></a>market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.tick.buckets.${buckets_tick}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20buckets_tick%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxTickTime')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_tick%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service,
    buckets_tick

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxTickTime')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    roundToExp2(duration_ms) as buckets_tick

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.nodejs.eventLoop.tick.buckets.%24%7Bbuckets_tick%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20buckets_tick%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxTickTime')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_tick%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.tick.buckets.${buckets_tick}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service,
        buckets_tick
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxTickTime')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        roundToExp2(duration_ms) as buckets_tick
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e819c0a653299bdae5903da6a5226d59'></a>market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.lag.buckets.${buckets_lag}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20buckets_lag%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxLag')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_lag%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service,
    buckets_lag

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxLag')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    roundToExp2(duration_ms) as buckets_lag

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.nodejs.eventLoop.lag.buckets.%24%7Bbuckets_lag%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20buckets_lag%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'eventLoop'%20and%20type%20%3D%20'maxLag')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_lag%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.lag.buckets.${buckets_lag}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service,
        buckets_lag
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxLag')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        roundToExp2(duration_ms) as buckets_lag
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a4d0c18e827c7064510e23fec7f01818'></a>market-front-unified.market_frontend_timers.v1.${service}.nodejs.boredom.buckets.${buckets_boredom}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20buckets_boredom%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'boredom'%20and%20type%20%3D%20'total')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_boredom%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service,
    buckets_boredom

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'boredom' and type = 'total')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    roundToExp2(duration_ms) as buckets_boredom

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.nodejs.boredom.buckets.%24%7Bbuckets_boredom%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20buckets_boredom%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'boredom'%20and%20type%20%3D%20'total')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_boredom%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.nodejs.boredom.buckets.${buckets_boredom}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service,
        buckets_boredom
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'boredom' and type = 'total')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        roundToExp2(duration_ms) as buckets_boredom
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9027481d4c256ab782a8578e569be785'></a>market-front-unified.market_frontend_timers.v1.${service}.nodejs.render.buckets.${buckets_render}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20buckets_render%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'render'%20and%20type%20%3D%20'total')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_render%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service,
    buckets_render

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'render' and type = 'total')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    roundToExp2(duration_ms) as buckets_render

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.nodejs.render.buckets.%24%7Bbuckets_render%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20buckets_render%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20label%20%3D%20'render'%20and%20type%20%3D%20'total')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_render%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.nodejs.render.buckets.${buckets_render}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service,
        buckets_render
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'render' and type = 'total')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        roundToExp2(duration_ms) as buckets_render
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c883627cec4621e4f6278665abfdf8b7'></a>market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-stuffing')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service,
    page,
    widget

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.widgets.%24%7Bpage%7D.%24%7Bwidget%7D.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-stuffing')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service,
        page,
        widget
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ba58a97f55a43507fa6b274f367c0189'></a>market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-stuffing')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service,
    page,
    widget,
    buckets_stuffing

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    roundToExp2(duration_ms) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.widgets.%24%7Bpage%7D.%24%7Bwidget%7D.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-stuffing')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        roundToExp2(duration_ms) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8c3b34cbd0d3ddec21530dabc4239895'></a>market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shipping.buckets.${buckets_shipping}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_shipping%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shipping')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_shipping%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service,
    page,
    widget,
    buckets_shipping

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shipping')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    roundToExp2(duration_ms) as buckets_shipping

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.widgets.%24%7Bpage%7D.%24%7Bwidget%7D.shipping.buckets.%24%7Bbuckets_shipping%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_shipping%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shipping')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_shipping%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shipping.buckets.${buckets_shipping}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service,
        page,
        widget,
        buckets_shipping
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shipping')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        roundToExp2(duration_ms) as buckets_shipping
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3ebfcd3c4a5bf6bf74521988187e02ba'></a>market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.rendering.buckets.${buckets_rendering}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_rendering%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-rendering')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_rendering%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service,
    page,
    widget,
    buckets_rendering

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-rendering')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    roundToExp2(duration_ms) as buckets_rendering

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.widgets.%24%7Bpage%7D.%24%7Bwidget%7D.rendering.buckets.%24%7Bbuckets_rendering%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_rendering%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-rendering')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_rendering%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.rendering.buckets.${buckets_rendering}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service,
        page,
        widget,
        buckets_rendering
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-rendering')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        roundToExp2(duration_ms) as buckets_rendering
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f52abba6b0994be0c834320612b8ff8b'></a>market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shaping.buckets.${buckets_shaping}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_shaping%0A%0AFROM%20market.market_frontend_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shaping')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_shaping%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service,
    page,
    widget,
    buckets_shaping

FROM market.market_frontend_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shaping')

GROUP BY metric_ts,
    transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    roundToExp2(duration_ms) as buckets_shaping

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_frontend_timers.v1.%24%7Bservice%7D.widgets.%24%7Bpage%7D.%24%7Bwidget%7D.shaping.buckets.%24%7Bbuckets_shaping%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_shaping%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_frontend_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20extract(nanny_service_id%2C%20'robots')%20%3D%20''%20and%20service%20!%3D%20'undefined_service'%20and%20page_id%20!%3D%20''%20and%20type%20!%3D%20'total'%20and%20label%20%3D%20'widget-shaping')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20transform(service%2C%20%5B'market_front_desktop'%2C'market_front_touch'%2C'market_front_black_desktop'%2C'market_front_blue_desktop'%2C'market_front_blue_touch'%2C'market_front_api'%2C'market_front_partner'%2C'market_front_vendors'%2C'market_front_affiliate'%2C'market_front_marketcorp'%2C'market_b2b-fapi'%5D%2C%20%5B'white_desktop'%2C'white_touch'%2C'black_desktop'%2C'blue_desktop'%2C'blue_touch'%2C'blue_fapi'%2C'partner_desktop'%2C'vendors_desktop'%2C'affiliate_desktop'%2C'corpsite_desktop'%2C'b2b_fapi'%5D%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20roundToExp2(duration_ms)%20as%20buckets_shaping%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shaping.buckets.${buckets_shaping}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service,
        page,
        widget,
        buckets_shaping
    
    FROM market.market_frontend_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shaping')
    
    GROUP BY metric_ts,
        transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        roundToExp2(duration_ms) as buckets_shaping
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```


## Overall Diagnostics

### Portion #1

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.tick.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxTickTime') as value_0, service FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxTickTime') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.lag.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxLag') as value_0, service FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxLag') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.nodejs.boredom.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'boredom' and type = 'total') as value_0, service FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'boredom' and type = 'total') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.nodejs.render.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'render' and type = 'total') as value_0, service FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'render' and type = 'total') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing') as value_0, service, page, widget FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shipping.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shipping') as value_0, service, page, widget FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shipping') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.rendering.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-rendering') as value_0, service, page, widget FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-rendering') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shaping.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shaping') as value_0, service, page, widget FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shaping') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.tick.buckets.${buckets_tick}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service, buckets_tick FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxTickTime') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, roundToExp2(duration_ms) as buckets_tick ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.nodejs.eventLoop.lag.buckets.${buckets_lag}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service, buckets_lag FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'eventLoop' and type = 'maxLag') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, roundToExp2(duration_ms) as buckets_lag ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.nodejs.boredom.buckets.${buckets_boredom}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service, buckets_boredom FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'boredom' and type = 'total') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, roundToExp2(duration_ms) as buckets_boredom ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.nodejs.render.buckets.${buckets_render}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service, buckets_render FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and label = 'render' and type = 'total') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, roundToExp2(duration_ms) as buckets_render ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service, page, widget FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service, page, widget, buckets_stuffing FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-stuffing') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, roundToExp2(duration_ms) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shipping.buckets.${buckets_shipping}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service, page, widget, buckets_shipping FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shipping') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, roundToExp2(duration_ms) as buckets_shipping ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.rendering.buckets.${buckets_rendering}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service, page, widget, buckets_rendering FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-rendering') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, roundToExp2(duration_ms) as buckets_rendering ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_frontend_timers.v1.${service}.widgets.${page}.${widget}.shaping.buckets.${buckets_shaping}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service, page, widget, buckets_shaping FROM market.market_frontend_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and extract(nanny_service_id, 'robots') = '' and service != 'undefined_service' and page_id != '' and type != 'total' and label = 'widget-shaping') GROUP BY metric_ts, transform(service, ['market_front_desktop','market_front_touch','market_front_black_desktop','market_front_blue_desktop','market_front_blue_touch','market_front_api','market_front_partner','market_front_vendors','market_front_affiliate','market_front_marketcorp','market_b2b-fapi'], ['white_desktop','white_touch','black_desktop','blue_desktop','blue_touch','blue_fapi','partner_desktop','vendors_desktop','affiliate_desktop','corpsite_desktop','b2b_fapi'], 'undefined_service' ) as service, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, roundToExp2(duration_ms) as buckets_shaping ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

