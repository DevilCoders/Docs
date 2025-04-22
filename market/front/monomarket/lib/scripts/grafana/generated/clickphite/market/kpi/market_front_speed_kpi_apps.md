# market/kpi/market_front_speed_kpi_apps
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `market_client_timers`

## Splits

```json
{
    "apps": "platform"
}
```

## Filters

```json
[
    "service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web'"
]
```

## Resulting metrics

  * [`market-front-unified.speed_kpi_apps.v1.${apps}.cart`](#cb2e140a6043f3463e493ff58731e660)
  * [`market-front-unified.speed_kpi_apps.v1.${apps}.catalog`](#07ff947f7fd6ac3b039f94b37a2ca95f)
  * [`market-front-unified.speed_kpi_apps.v1.${apps}.main`](#78615cda9fd69d4bf5f3a06f0c29cfb5)
  * [`market-front-unified.speed_kpi_apps.v1.${apps}.requests`](#04f87619ded87d757734a8af3fa59821)
  * [`market-front-unified.speed_kpi_apps.v1.${apps}.search`](#389cb287abdc1fcfed9fa87981a6b844)
  * [`market-front-unified.speed_kpi_apps.v1.${apps}.sku`](#7ed1c63bebfc3c4f81ddd6b2880402e6)

## Metrics

#### <a id='04f87619ded87d757734a8af3fa59821'></a>market-front-unified.speed_kpi_apps.v1.${apps}.requests

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20as%20value_0%2C%0A%20%20%20%20apps%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20platform%20as%20apps%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() as value_0,
    apps

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')

GROUP BY metric_ts,
    platform as apps

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.speed_kpi_apps.v1.%24%7Bapps%7D.requests'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20apps%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20platform%20as%20apps%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.speed_kpi_apps.v1.${apps}.requests' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() as value_0,
        apps
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')
    
    GROUP BY metric_ts,
        platform as apps
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='78615cda9fd69d4bf5f3a06f0c29cfb5'></a>market-front-unified.speed_kpi_apps.v1.${apps}.main

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantileTimingIf(0.95)(duration_ms%2C%20portion%3D'PROMO_SCREEN')%20as%20value_0%2C%0A%20%20%20%20apps%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20platform%20as%20apps%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantileTimingIf(0.95)(duration_ms, portion='PROMO_SCREEN') as value_0,
    apps

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')

GROUP BY metric_ts,
    platform as apps

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.speed_kpi_apps.v1.%24%7Bapps%7D.main'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantileTimingIf(0.95)(duration_ms%2C%20portion%3D'PROMO_SCREEN')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20apps%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20platform%20as%20apps%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.speed_kpi_apps.v1.${apps}.main' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantileTimingIf(0.95)(duration_ms, portion='PROMO_SCREEN') as value_0,
        apps
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')
    
    GROUP BY metric_ts,
        platform as apps
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='cb2e140a6043f3463e493ff58731e660'></a>market-front-unified.speed_kpi_apps.v1.${apps}.cart

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantileTimingIf(0.95)(duration_ms%2C%20portion%3D'CART_SCREEN')%20as%20value_0%2C%0A%20%20%20%20apps%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20platform%20as%20apps%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantileTimingIf(0.95)(duration_ms, portion='CART_SCREEN') as value_0,
    apps

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')

GROUP BY metric_ts,
    platform as apps

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.speed_kpi_apps.v1.%24%7Bapps%7D.cart'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantileTimingIf(0.95)(duration_ms%2C%20portion%3D'CART_SCREEN')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20apps%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20platform%20as%20apps%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.speed_kpi_apps.v1.${apps}.cart' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantileTimingIf(0.95)(duration_ms, portion='CART_SCREEN') as value_0,
        apps
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')
    
    GROUP BY metric_ts,
        platform as apps
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7ed1c63bebfc3c4f81ddd6b2880402e6'></a>market-front-unified.speed_kpi_apps.v1.${apps}.sku

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantileTimingIf(0.95)(duration_ms%2C%20portion%3D'SKU_SCREEN')%20as%20value_0%2C%0A%20%20%20%20apps%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20platform%20as%20apps%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantileTimingIf(0.95)(duration_ms, portion='SKU_SCREEN') as value_0,
    apps

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')

GROUP BY metric_ts,
    platform as apps

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.speed_kpi_apps.v1.%24%7Bapps%7D.sku'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantileTimingIf(0.95)(duration_ms%2C%20portion%3D'SKU_SCREEN')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20apps%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20platform%20as%20apps%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.speed_kpi_apps.v1.${apps}.sku' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantileTimingIf(0.95)(duration_ms, portion='SKU_SCREEN') as value_0,
        apps
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')
    
    GROUP BY metric_ts,
        platform as apps
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='389cb287abdc1fcfed9fa87981a6b844'></a>market-front-unified.speed_kpi_apps.v1.${apps}.search

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantileTimingIf(0.95)(duration_ms%2C%20portion%3D'SEARCH_RESULT_SCREEN')%20as%20value_0%2C%0A%20%20%20%20apps%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20platform%20as%20apps%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantileTimingIf(0.95)(duration_ms, portion='SEARCH_RESULT_SCREEN') as value_0,
    apps

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')

GROUP BY metric_ts,
    platform as apps

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.speed_kpi_apps.v1.%24%7Bapps%7D.search'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantileTimingIf(0.95)(duration_ms%2C%20portion%3D'SEARCH_RESULT_SCREEN')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20apps%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20platform%20as%20apps%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.speed_kpi_apps.v1.${apps}.search' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantileTimingIf(0.95)(duration_ms, portion='SEARCH_RESULT_SCREEN') as value_0,
        apps
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')
    
    GROUP BY metric_ts,
        platform as apps
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='07ff947f7fd6ac3b039f94b37a2ca95f'></a>market-front-unified.speed_kpi_apps.v1.${apps}.catalog

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantileTimingIf(0.95)(duration_ms%2C%20portion%3D'ROOT_CATALOG_SCREEN'%20or%20portion%3D'CATALOG_SCREEN')%20as%20value_0%2C%0A%20%20%20%20apps%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20platform%20as%20apps%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantileTimingIf(0.95)(duration_ms, portion='ROOT_CATALOG_SCREEN' or portion='CATALOG_SCREEN') as value_0,
    apps

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')

GROUP BY metric_ts,
    platform as apps

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.speed_kpi_apps.v1.%24%7Bapps%7D.catalog'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantileTimingIf(0.95)(duration_ms%2C%20portion%3D'ROOT_CATALOG_SCREEN'%20or%20portion%3D'CATALOG_SCREEN')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20apps%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(service%20%3D%20'market_front_bluetouch'%20and%20name%3D'SCREEN_OPENED_MAIN_COMPONENT'%20and%20regionToCountry(region)%20%3D%20225%20and%20platform%20!%3D%20'web')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20platform%20as%20apps%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.speed_kpi_apps.v1.${apps}.catalog' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantileTimingIf(0.95)(duration_ms, portion='ROOT_CATALOG_SCREEN' or portion='CATALOG_SCREEN') as value_0,
        apps
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web')
    
    GROUP BY metric_ts,
        platform as apps
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```


## Overall Diagnostics

### Portion #1

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.speed_kpi_apps.v1.${apps}.requests' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() as value_0, apps FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web') GROUP BY metric_ts, platform as apps ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.speed_kpi_apps.v1.${apps}.main' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantileTimingIf(0.95)(duration_ms, portion='PROMO_SCREEN') as value_0, apps FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web') GROUP BY metric_ts, platform as apps ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.speed_kpi_apps.v1.${apps}.cart' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantileTimingIf(0.95)(duration_ms, portion='CART_SCREEN') as value_0, apps FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web') GROUP BY metric_ts, platform as apps ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.speed_kpi_apps.v1.${apps}.sku' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantileTimingIf(0.95)(duration_ms, portion='SKU_SCREEN') as value_0, apps FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web') GROUP BY metric_ts, platform as apps ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.speed_kpi_apps.v1.${apps}.search' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantileTimingIf(0.95)(duration_ms, portion='SEARCH_RESULT_SCREEN') as value_0, apps FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web') GROUP BY metric_ts, platform as apps ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.speed_kpi_apps.v1.${apps}.catalog' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantileTimingIf(0.95)(duration_ms, portion='ROOT_CATALOG_SCREEN' or portion='CATALOG_SCREEN') as value_0, apps FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (service = 'market_front_bluetouch' and name='SCREEN_OPENED_MAIN_COMPONENT' and regionToCountry(region) = 225 and platform != 'web') GROUP BY metric_ts, platform as apps ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

