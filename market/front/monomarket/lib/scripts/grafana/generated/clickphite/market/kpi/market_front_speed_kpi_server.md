# market/kpi/market_front_speed_kpi_server
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `nginx2`

## Splits

```json
{
    "service": "multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch',vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' )",
    "requester": "arrayJoin(['any-requester', multiIf(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\\\)|MSRBOT \\\\(http://research\\\\.microsoft\\\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\\\.com|Refer\\\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in')])",
    "requestType": "arrayJoin(['any-type', if(splitByChar(':', page_id)[1] = 'api', 'api', 'page')])"
}
```

## Filters

```json
[
    "dynamic = 1 and http_code = 200 and environment = 'PRODUCTION' and url != '/ping' and service != 'undefined_service'"
]
```

## Resulting metrics

  * [`market-front-unified.speed_kpi_server.v1.${service}.${requester}.${requestType}.requests`](#a60162f5ec5caeeb1b8ca594c940363a)
  * [`market-front-unified.speed_kpi_server.v1.${service}.${requester}.${requestType}.ttlb`](#5798b90e218452a39d9a4822fdac9b58)

## Metrics

#### <a id='a60162f5ec5caeeb1b8ca594c940363a'></a>market-front-unified.speed_kpi_server.v1.${service}.${requester}.${requestType}.requests

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20requestType%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(dynamic%20%3D%201%20and%20http_code%20%3D%20200%20and%20environment%20%3D%20'PRODUCTION'%20and%20url%20!%3D%20'%2Fping'%20and%20service%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%2Cvhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20arrayJoin(%5B'any-requester'%2C%20multiIf(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%5D)%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-type'%2C%20if(splitByChar('%3A'%2C%20page_id)%5B1%5D%20%3D%20'api'%2C%20'api'%2C%20'page')%5D)%20as%20requestType%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() as value_0,
    service,
    requester,
    requestType

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (dynamic = 1 and http_code = 200 and environment = 'PRODUCTION' and url != '/ping' and service != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch',vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service,
    arrayJoin(['any-requester', multiIf(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in')]) as requester,
    arrayJoin(['any-type', if(splitByChar(':', page_id)[1] = 'api', 'api', 'page')]) as requestType

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.speed_kpi_server.v1.%24%7Bservice%7D.%24%7Brequester%7D.%24%7BrequestType%7D.requests'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20requestType%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(dynamic%20%3D%201%20and%20http_code%20%3D%20200%20and%20environment%20%3D%20'PRODUCTION'%20and%20url%20!%3D%20'%2Fping'%20and%20service%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%2Cvhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-requester'%2C%20multiIf(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%5D)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-type'%2C%20if(splitByChar('%3A'%2C%20page_id)%5B1%5D%20%3D%20'api'%2C%20'api'%2C%20'page')%5D)%20as%20requestType%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.speed_kpi_server.v1.${service}.${requester}.${requestType}.requests' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() as value_0,
        service,
        requester,
        requestType
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (dynamic = 1 and http_code = 200 and environment = 'PRODUCTION' and url != '/ping' and service != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch',vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service,
        arrayJoin(['any-requester', multiIf(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in')]) as requester,
        arrayJoin(['any-type', if(splitByChar(':', page_id)[1] = 'api', 'api', 'page')]) as requestType
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5798b90e218452a39d9a4822fdac9b58'></a>market-front-unified.speed_kpi_server.v1.${service}.${requester}.${requestType}.ttlb

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantileTiming(0.99)(resptime_ms)%20as%20value_0%2C%0A%20%20%20%20service%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20requestType%0A%0AFROM%20market.nginx2%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(dynamic%20%3D%201%20and%20http_code%20%3D%20200%20and%20environment%20%3D%20'PRODUCTION'%20and%20url%20!%3D%20'%2Fping'%20and%20service%20!%3D%20'undefined_service')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%2Cvhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20arrayJoin(%5B'any-requester'%2C%20multiIf(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%5D)%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-type'%2C%20if(splitByChar('%3A'%2C%20page_id)%5B1%5D%20%3D%20'api'%2C%20'api'%2C%20'page')%5D)%20as%20requestType%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantileTiming(0.99)(resptime_ms) as value_0,
    service,
    requester,
    requestType

FROM market.nginx2

WHERE date = today() and timestamp > now() - 60 * 60
    AND (dynamic = 1 and http_code = 200 and environment = 'PRODUCTION' and url != '/ping' and service != 'undefined_service')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch',vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service,
    arrayJoin(['any-requester', multiIf(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in')]) as requester,
    arrayJoin(['any-type', if(splitByChar(':', page_id)[1] = 'api', 'api', 'page')]) as requestType

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.speed_kpi_server.v1.%24%7Bservice%7D.%24%7Brequester%7D.%24%7BrequestType%7D.ttlb'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantileTiming(0.99)(resptime_ms)%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20requestType%0A%20%20%20%20%0A%20%20%20%20FROM%20market.nginx2%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(dynamic%20%3D%201%20and%20http_code%20%3D%20200%20and%20environment%20%3D%20'PRODUCTION'%20and%20url%20!%3D%20'%2Fping'%20and%20service%20!%3D%20'undefined_service')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%2Cvhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-requester'%2C%20multiIf(extract(user_agent%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%5D)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-type'%2C%20if(splitByChar('%3A'%2C%20page_id)%5B1%5D%20%3D%20'api'%2C%20'api'%2C%20'page')%5D)%20as%20requestType%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.speed_kpi_server.v1.${service}.${requester}.${requestType}.ttlb' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantileTiming(0.99)(resptime_ms) as value_0,
        service,
        requester,
        requestType
    
    FROM market.nginx2
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (dynamic = 1 and http_code = 200 and environment = 'PRODUCTION' and url != '/ping' and service != 'undefined_service')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch',vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service,
        arrayJoin(['any-requester', multiIf(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in')]) as requester,
        arrayJoin(['any-type', if(splitByChar(':', page_id)[1] = 'api', 'api', 'page')]) as requestType
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```


## Overall Diagnostics

### Portion #1

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.speed_kpi_server.v1.${service}.${requester}.${requestType}.requests' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() as value_0, service, requester, requestType FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (dynamic = 1 and http_code = 200 and environment = 'PRODUCTION' and url != '/ping' and service != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch',vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service, arrayJoin(['any-requester', multiIf(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in')]) as requester, arrayJoin(['any-type', if(splitByChar(':', page_id)[1] = 'api', 'api', 'page')]) as requestType ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.speed_kpi_server.v1.${service}.${requester}.${requestType}.ttlb' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantileTiming(0.99)(resptime_ms) as value_0, service, requester, requestType FROM market.nginx2 WHERE date = today() and timestamp > now() - 60 * 60 AND (dynamic = 1 and http_code = 200 and environment = 'PRODUCTION' and url != '/ping' and service != 'undefined_service') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch',vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service, arrayJoin(['any-requester', multiIf(extract(user_agent,'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in')]) as requester, arrayJoin(['any-type', if(splitByChar(':', page_id)[1] = 'api', 'api', 'page')]) as requestType ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

