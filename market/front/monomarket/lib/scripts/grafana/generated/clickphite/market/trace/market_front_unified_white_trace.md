# market/trace/market_front_unified_white_trace
    
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
    "environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_desktop'",
    "environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != ''",
    "environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_desktop' and region != ''",
    "environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_touch'",
    "environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != ''",
    "environment = 'PRODUCTION' and module = 'market_front_touch' and region != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_touch' and region != ''",
    "environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_touch_api'",
    "environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != ''",
    "environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '' and error_code != ''",
    "environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != ''"
]
```

## Resulting metrics

  * [`market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#b351257df5c8e8fb30b9d5a177c2d559)
  * [`market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps`](#0a90cf3d1d00bec4b16c7c59017d7b42)
  * [`market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#0afb14035aac0bd9d89c668813a91ab5)
  * [`market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#51f9070a82ee3e4e638abeb052388ad2)
  * [`market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps`](#8ba62e3693e37e61931d985833cfb971)
  * [`market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#311cf5078cd94f00532be671fe25aaed)
  * [`market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps`](#3c0904882b25384c13783ff3729b0013)
  * [`market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#d50cca190ec51f349f67200378af2566)
  * [`market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#d18859e4a1abc9f118088d8b7ebe06ad)
  * [`market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps`](#617b6a09f028f2c6e0cb77423dcdf9d2)
  * [`market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#cfa2158d64d822716b0a458c4b97d942)
  * [`market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#0f974b746806db92225435aa4cf477ec)
  * [`market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps`](#5edcb3178d026b2d92694a488b85bc0f)
  * [`market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#28d8f3ac918487e9dbf41e06255a22ae)
  * [`market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps`](#3e152ab86c8184bd2a3f2e552e601c52)
  * [`market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#f988f21a54fec85ec8678c23dc6143c6)
  * [`market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#e96eb7804e911ebc7978e8f014bd8ea9)
  * [`market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps`](#8324f778c936dd80943984976adc193d)
  * [`market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#b3de782498375893983eac9d13ff5c8b)
  * [`market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#0a76bc66d25472bf512bb5c221503979)
  * [`market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps`](#c66c0b09dda928ef758c8bf457213ded)
  * [`market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#8688f5c4bb9205a8720542d91aa3aa83)
  * [`market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps`](#458c01fd401c5124980d76a893756b00)
  * [`market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#178ea99eb4ff436b872f4c9fef2e6dba)
  * [`market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#b5d5d7ba1dd710a0f93ddbe04d3f34a7)
  * [`market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps`](#107cb1fcf998697a0098d556e1eeb4ec)
  * [`market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#f97ce7c797e72801b86c836051fd398b)
  * [`market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#60fc68300777279651760facb1bf3d3f)
  * [`market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps`](#1127242bddf1d6abb3a335eef47bb014)
  * [`market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#bb1ec59fdd54b25694828229a951b105)
  * [`market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps`](#243f9114680722bf03fa43c4aa4107ed)
  * [`market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#9924eee1187f952d4aa8339ca96fdb17)
  * [`market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#fcc40f8cefc55cc8a1d5753d2c915d56)
  * [`market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps`](#2c18b8573ea9ed93db0b466153ae62f5)
  * [`market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#51a0c1ed99259e60bd7819341830938b)
  * [`market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#7581d6ee556091399bc502797a506480)
  * [`market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps`](#9deb5355042bafd3158fd17e88cf08f3)
  * [`market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#c42c09ed32ed797e086267b95446c68f)
  * [`market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps`](#24528416c7cf2ef22cb64ef85dee4c0b)
  * [`market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#32fc06d6d06369d6305b7c16007106d1)
  * [`market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#5549d0afee7cd7da3daeaf59719b210a)
  * [`market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps`](#8dae683a1aa82c47347e7643c352c670)
  * [`market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#e7e7ea97386b31cfd07c2e6387df44db)
  * [`market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#05cdef4d5a458cc6f56825870c750351)
  * [`market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps`](#32494a8e5c46af64d0db498ffbbc169a)
  * [`market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#9c19cf4d8d80931db7f391d356a343b9)
  * [`market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps`](#f995c2afd734a6f33c153c8c2a6cab6e)
  * [`market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#50d671b2fcaa3e412a491fb46c3bbb54)
  * [`market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#342b035f86d795159dcdb65a4426f529)
  * [`market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps`](#ad0d7cd3da9fa4c454a29defae40c915)
  * [`market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#3a8b9f67b37874cf92a71327445c5336)
  * [`market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#4197c39d58b7ffc307a4c1377c077f8a)
  * [`market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps`](#bdc6b6dd980a9281b8c9b76cb1725cbe)
  * [`market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#cf22fc675515749a3a78cc9691bb366b)
  * [`market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps`](#c5951fc3eebd5de4ae1072b3d4d06519)
  * [`market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#890c2021a38e67cf00729203641c437a)
  * [`market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#ddbd900b596e4263525301f2dc6544c8)
  * [`market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps`](#fd28ea110c37ff2c6b55d0dcd9d6691d)
  * [`market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#c95594dbcb54ac55533fa0c77cc6f0e8)
  * [`market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#6bd6982743d822f724a0fc0107a3cd76)
  * [`market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps`](#678856d9eb0d14cd977773ef26480945)
  * [`market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#ee374ea19656f33fc0a2db5abcd5b1d9)
  * [`market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps`](#2306d5225f66ad6eccd689467f9b5165)
  * [`market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#8fea48ff50b7be9db6689a1878b1a992)
  * [`market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#54a255581963941e074cd7f856670454)
  * [`market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps`](#48dd71a868c1feb8af5555eba4cfb223)
  * [`market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#467613b02d97d31ca59ff9eef7e93b68)
  * [`market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#9faa98411850298e3c3c1aeafc790b39)
  * [`market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps`](#7d154b86ca180b083f49dcd4ecf39dff)
  * [`market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#b0b080198cf1626b92d823cf2eb42608)
  * [`market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps`](#4f11bcf9f49652fa1017c9b714b1f6d5)
  * [`market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#a0cedb8c41a1057709f4137b17390496)
  * [`market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#2a218aaf66f4a002e1d6e037efaca8a1)
  * [`market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps`](#a4eb935d40684d268b7888db1449918d)
  * [`market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#08b4172e5091c589a232c3b193ca058d)
  * [`market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#094b1ea53d1d843e57fac45739a8cbea)
  * [`market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps`](#d60109e6355ce245a9b4dc75507b1a9e)
  * [`market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#7fb5a2cc9f5ec2501fcd6d83a6af9208)
  * [`market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps`](#15408e03fef6ecbe5073ac8808b39b9f)
  * [`market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#0d902b1718c737d061d96ffb114a8987)
  * [`market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#dddddd5d61cbf80670d9c2a32b3499f5)
  * [`market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps`](#165906877f55b607682e8dc764a478d0)
  * [`market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#eb866fffd4307f6944d4da8b03c65ed5)
  * [`market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#489b6745f0553b48bd21c228e3cb5313)
  * [`market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps`](#c96e9aacbe32d8be710da10ce5d9b4cf)
  * [`market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#19d20d767273c1a6a6d943bf853e36b7)
  * [`market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps`](#0404db3c2e94fc155de9f755857aebe7)
  * [`market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#a2fd870f8e0b92c7a4764c0f7af82998)
  * [`market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#7f355cc434f2f352f9b0d0bbf45de1d0)
  * [`market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.rps`](#c02def7caea58b9530c70a99ef01108f)
  * [`market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#d08105df734fbdcea16eeea37ae1b62f)
  * [`market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#1595cec6b9f22ad870206e1bc4d0eb17)
  * [`market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.rps`](#59ad4ced70bda33df23fe32c57335f66)
  * [`market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#ad0c462e98a48c70143a47716eac9339)
  * [`market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.error.any-error.metrics.rps`](#cc873399d4807cd70de2f6e48137311b)
  * [`market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#3fe6ca7223993efbefce07d5fb87bbc2)
  * [`market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#c72379f043e9c337336007024f9439fd)
  * [`market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps`](#3d40c4e7840414a4017c17d45310afac)
  * [`market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#bd343b880996bc219c425b80defd2e85)
  * [`market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#c97db330cccbc352fa2964361b108979)
  * [`market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps`](#99df54eec43d9eb07a892675409bcf08)
  * [`market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#5c225760969489c8aa56fdc3b2369cfa)
  * [`market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps`](#f576dcbffeeb2f56e5d976e0111b7b69)
  * [`market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#d1d1bd692f073ed4bc6f4faad31baecb)
  * [`market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#92163fd90b55d621765456de3c80a13d)
  * [`market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps`](#6dc16c1c9aabfa08a78e54909797d6eb)
  * [`market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#3d4345a4584656a542d35980accf2b96)
  * [`market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#9db1e7b5341fd3d964735b8b0d3354e1)
  * [`market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps`](#42eb0ae5628342a3771f39b4bc51e88d)
  * [`market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#76bc45326181adc040c6509f6f1788dc)
  * [`market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps`](#39c1c8e34b01e97ec6d6f82a64fe33d9)
  * [`market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#5c5b47484f7f4185965f16a840dece61)
  * [`market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#21417b154db20aa4aa7fb18363f52e48)
  * [`market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps`](#37333d4f2c23e17546df140759638e52)
  * [`market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#fc48e1a4c8c08a42f51b379d2f7a37f6)
  * [`market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#76c0157577073e6d1baebc3b778dd527)
  * [`market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps`](#3b9cdf63644f3284813c21e08b563a29)
  * [`market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#38d11d192415b9ce87ef893e6f6230f3)
  * [`market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps`](#7324aadc56959b8f949a5f6e8d161afb)
  * [`market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#0b05a93f61bf316675734002b4079cd2)
  * [`market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#198ecfec3070723860f6ceee8e471b19)
  * [`market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps`](#e0fb34f91efe24b41bc24ec7941b7242)
  * [`market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#43ddfa6b3c0781f8f1a5be4e1ba94e50)
  * [`market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#a3451d8653d565c245bd254d74e9bf41)
  * [`market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps`](#6a478ba26c2e01337b6b90e90e6bf431)
  * [`market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#a7b7a094f97ccab8bec99988aeda456e)
  * [`market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps`](#498df377a8f0d27ee7b9828fc8d1c69e)
  * [`market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#38b6e8d99647e93879cc6fd86c245d27)
  * [`market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#39773a70a2730c33810b84d05c75d709)
  * [`market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps`](#209a1e6cf9b252c50fa1bce45d323134)
  * [`market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#c463ae890ec555eb74c0f19b781d6aac)
  * [`market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#726f4a03ad315c27ec5efb73b61b74e4)
  * [`market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps`](#ebffbbc05eaab599ede501824f63f848)
  * [`market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#df144a46c60a1398b833175805ff0a4e)
  * [`market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps`](#8479475c6561e83ab776e47e557fae31)
  * [`market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#b967ceaf4031d81c8c4d403f3676ae7e)
  * [`market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles`](#6365ebc4d429f53531e241b21cfe09f8)
  * [`market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.rps`](#da395c5d6b30e988a7d32b16760f6764)
  * [`market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles`](#6ac4069f1476ec9da16100a1892b4270)
  * [`market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles`](#ec1f8cf5d3b7ec480bf5f2231d215ef7)
  * [`market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.rps`](#55004df57aa52f9430084cbfa0f9c4a3)
  * [`market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles`](#917b0214f29d896af0dfa7bc27b5f555)
  * [`market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.error.any-error.metrics.rps`](#70924ed2575231c4b7fd847e612bb859)
  * [`market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.error.split.${error}.metrics.rps`](#9faa850e3c4e1800d3306e47ae2ffcf9)

## Metrics

#### <a id='f995c2afd734a6f33c153c8c2a6cab6e'></a>market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='50d671b2fcaa3e412a491fb46c3bbb54'></a>market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3c0904882b25384c13783ff3729b0013'></a>market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d50cca190ec51f349f67200378af2566'></a>market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')
    
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
#### <a id='3e152ab86c8184bd2a3f2e552e601c52'></a>market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f988f21a54fec85ec8678c23dc6143c6'></a>market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')
    
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
#### <a id='24528416c7cf2ef22cb64ef85dee4c0b'></a>market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='32fc06d6d06369d6305b7c16007106d1'></a>market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '')
    
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
#### <a id='32494a8e5c46af64d0db498ffbbc169a'></a>market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8dae683a1aa82c47347e7643c352c670'></a>market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8ba62e3693e37e61931d985833cfb971'></a>market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0a90cf3d1d00bec4b16c7c59017d7b42'></a>market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
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
#### <a id='5edcb3178d026b2d92694a488b85bc0f'></a>market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='617b6a09f028f2c6e0cb77423dcdf9d2'></a>market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
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
#### <a id='9deb5355042bafd3158fd17e88cf08f3'></a>market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2c18b8573ea9ed93db0b466153ae62f5'></a>market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
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
#### <a id='458c01fd401c5124980d76a893756b00'></a>market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='178ea99eb4ff436b872f4c9fef2e6dba'></a>market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '' and error_code != '')
    
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
#### <a id='c66c0b09dda928ef758c8bf457213ded'></a>market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8324f778c936dd80943984976adc193d'></a>market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')
    
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
#### <a id='243f9114680722bf03fa43c4aa4107ed'></a>market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9924eee1187f952d4aa8339ca96fdb17'></a>market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '' and error_code != '')
    
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
#### <a id='1127242bddf1d6abb3a335eef47bb014'></a>market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='107cb1fcf998697a0098d556e1eeb4ec'></a>market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')
    
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
#### <a id='70924ed2575231c4b7fd847e612bb859'></a>market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9faa850e3c4e1800d3306e47ae2ffcf9'></a>market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f576dcbffeeb2f56e5d976e0111b7b69'></a>market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d1d1bd692f073ed4bc6f4faad31baecb'></a>market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')
    
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
#### <a id='39c1c8e34b01e97ec6d6f82a64fe33d9'></a>market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5c5b47484f7f4185965f16a840dece61'></a>market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')
    
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
#### <a id='8479475c6561e83ab776e47e557fae31'></a>market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b967ceaf4031d81c8c4d403f3676ae7e'></a>market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '')
    
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
#### <a id='55004df57aa52f9430084cbfa0f9c4a3'></a>market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='da395c5d6b30e988a7d32b16760f6764'></a>market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='99df54eec43d9eb07a892675409bcf08'></a>market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3d40c4e7840414a4017c17d45310afac'></a>market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
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
#### <a id='42eb0ae5628342a3771f39b4bc51e88d'></a>market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6dc16c1c9aabfa08a78e54909797d6eb'></a>market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
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
#### <a id='ebffbbc05eaab599ede501824f63f848'></a>market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='209a1e6cf9b252c50fa1bce45d323134'></a>market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
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
#### <a id='7324aadc56959b8f949a5f6e8d161afb'></a>market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0b05a93f61bf316675734002b4079cd2'></a>market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '' and error_code != '')
    
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
#### <a id='3b9cdf63644f3284813c21e08b563a29'></a>market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='37333d4f2c23e17546df140759638e52'></a>market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')
    
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
#### <a id='498df377a8f0d27ee7b9828fc8d1c69e'></a>market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='38b6e8d99647e93879cc6fd86c245d27'></a>market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '' and error_code != '')
    
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
#### <a id='6a478ba26c2e01337b6b90e90e6bf431'></a>market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e0fb34f91efe24b41bc24ec7941b7242'></a>market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')
    
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
#### <a id='cc873399d4807cd70de2f6e48137311b'></a>market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3fe6ca7223993efbefce07d5fb87bbc2'></a>market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    error

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c5951fc3eebd5de4ae1072b3d4d06519'></a>market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='890c2021a38e67cf00729203641c437a'></a>market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')
    
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
#### <a id='2306d5225f66ad6eccd689467f9b5165'></a>market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8fea48ff50b7be9db6689a1878b1a992'></a>market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')
    
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
#### <a id='0404db3c2e94fc155de9f755857aebe7'></a>market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a2fd870f8e0b92c7a4764c0f7af82998'></a>market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '')
    
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
#### <a id='59ad4ced70bda33df23fe32c57335f66'></a>market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c02def7caea58b9530c70a99ef01108f'></a>market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bdc6b6dd980a9281b8c9b76cb1725cbe'></a>market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ad0d7cd3da9fa4c454a29defae40c915'></a>market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
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
#### <a id='678856d9eb0d14cd977773ef26480945'></a>market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fd28ea110c37ff2c6b55d0dcd9d6691d'></a>market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
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
#### <a id='c96e9aacbe32d8be710da10ce5d9b4cf'></a>market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='165906877f55b607682e8dc764a478d0'></a>market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
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
#### <a id='4f11bcf9f49652fa1017c9b714b1f6d5'></a>market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a0cedb8c41a1057709f4137b17390496'></a>market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '' and error_code != '')
    
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
#### <a id='7d154b86ca180b083f49dcd4ecf39dff'></a>market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='48dd71a868c1feb8af5555eba4cfb223'></a>market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')
    
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
#### <a id='15408e03fef6ecbe5073ac8808b39b9f'></a>market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.any-error.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '' and error_code != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0d902b1718c737d061d96ffb114a8987'></a>market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20error%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '' and error_code != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.error.split.%24%7Berror%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20error%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20''%20and%20error_code%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(error_code%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'_')%20as%20error%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '' and error_code != '')
    
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
#### <a id='d60109e6355ce245a9b4dc75507b1a9e'></a>market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a4eb935d40684d268b7888db1449918d'></a>market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
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
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.rps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, 
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
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')
    
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
#### <a id='9c19cf4d8d80931db7f391d356a343b9'></a>market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e7e7ea97386b31cfd07c2e6387df44db'></a>market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='311cf5078cd94f00532be671fe25aaed'></a>market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0afb14035aac0bd9d89c668813a91ab5'></a>market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
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
#### <a id='28d8f3ac918487e9dbf41e06255a22ae'></a>market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='cfa2158d64d822716b0a458c4b97d942'></a>market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
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
#### <a id='c42c09ed32ed797e086267b95446c68f'></a>market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='51a0c1ed99259e60bd7819341830938b'></a>market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
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
#### <a id='8688f5c4bb9205a8720542d91aa3aa83'></a>market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b3de782498375893983eac9d13ff5c8b'></a>market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')
    
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
#### <a id='bb1ec59fdd54b25694828229a951b105'></a>market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f97ce7c797e72801b86c836051fd398b'></a>market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')
    
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
#### <a id='917b0214f29d896af0dfa7bc27b5f555'></a>market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6ac4069f1476ec9da16100a1892b4270'></a>market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5c225760969489c8aa56fdc3b2369cfa'></a>market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bd343b880996bc219c425b80defd2e85'></a>market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
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
#### <a id='76bc45326181adc040c6509f6f1788dc'></a>market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3d4345a4584656a542d35980accf2b96'></a>market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
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
#### <a id='df144a46c60a1398b833175805ff0a4e'></a>market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c463ae890ec555eb74c0f19b781d6aac'></a>market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
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
#### <a id='38d11d192415b9ce87ef893e6f6230f3'></a>market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fc48e1a4c8c08a42f51b379d2f7a37f6'></a>market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')
    
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
#### <a id='a7b7a094f97ccab8bec99988aeda456e'></a>market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='43ddfa6b3c0781f8f1a5be4e1ba94e50'></a>market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')
    
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
#### <a id='ad0c462e98a48c70143a47716eac9339'></a>market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d08105df734fbdcea16eeea37ae1b62f'></a>market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='cf22fc675515749a3a78cc9691bb366b'></a>market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3a8b9f67b37874cf92a71327445c5336'></a>market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
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
#### <a id='ee374ea19656f33fc0a2db5abcd5b1d9'></a>market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c95594dbcb54ac55533fa0c77cc6f0e8'></a>market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
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
#### <a id='19d20d767273c1a6a6d943bf853e36b7'></a>market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='eb866fffd4307f6944d4da8b03c65ed5'></a>market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
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
#### <a id='b0b080198cf1626b92d823cf2eb42608'></a>market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='467613b02d97d31ca59ff9eef7e93b68'></a>market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')
    
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
#### <a id='7fb5a2cc9f5ec2501fcd6d83a6af9208'></a>market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='08b4172e5091c589a232c3b193ca058d'></a>market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.ttlb.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(duration_ms%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')
    
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
#### <a id='05cdef4d5a458cc6f56825870c750351'></a>market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5549d0afee7cd7da3daeaf59719b210a'></a>market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='51f9070a82ee3e4e638abeb052388ad2'></a>market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b351257df5c8e8fb30b9d5a177c2d559'></a>market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
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
#### <a id='0f974b746806db92225435aa4cf477ec'></a>market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d18859e4a1abc9f118088d8b7ebe06ad'></a>market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
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
#### <a id='7581d6ee556091399bc502797a506480'></a>market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fcc40f8cefc55cc8a1d5753d2c915d56'></a>market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop')
    
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
#### <a id='0a76bc66d25472bf512bb5c221503979'></a>market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e96eb7804e911ebc7978e8f014bd8ea9'></a>market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '')
    
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
#### <a id='60fc68300777279651760facb1bf3d3f'></a>market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b5d5d7ba1dd710a0f93ddbe04d3f34a7'></a>market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_desktop.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_desktop'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '')
    
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
#### <a id='ec1f8cf5d3b7ec480bf5f2231d215ef7'></a>market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6365ebc4d429f53531e241b21cfe09f8'></a>market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c97db330cccbc352fa2964361b108979'></a>market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c72379f043e9c337336007024f9439fd'></a>market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
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
#### <a id='9db1e7b5341fd3d964735b8b0d3354e1'></a>market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='92163fd90b55d621765456de3c80a13d'></a>market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
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
#### <a id='726f4a03ad315c27ec5efb73b61b74e4'></a>market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='39773a70a2730c33810b84d05c75d709'></a>market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch')
    
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
#### <a id='76c0157577073e6d1baebc3b778dd527'></a>market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='21417b154db20aa4aa7fb18363f52e48'></a>market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '')
    
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
#### <a id='a3451d8653d565c245bd254d74e9bf41'></a>market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='198ecfec3070723860f6ceee8e471b19'></a>market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_touch.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '')
    
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
#### <a id='1595cec6b9f22ad870206e1bc4d0eb17'></a>market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7f355cc434f2f352f9b0d0bbf45de1d0'></a>market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.total.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
        concat(substring(toString(http_code),1,1),'xx') as code
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4197c39d58b7ffc307a4c1377c077f8a'></a>market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    dc,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        dc,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='342b035f86d795159dcdb65a4426f529'></a>market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20dc%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    dc,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.dc.splits.%24%7Bdc%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20dc%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20substring(host%2C%201%2C%203)%20in%20('iva'%2C%20'man'%2C%20'vla'%2C%20'sas'%2C%20'myt')%2C%20substring(host%2C%201%2C%203)%2C%20endsWith(host%2C%20'yp-c.yandex.net')%2C%20substring(host%2C%20position(host%2C%20'.')%20%2B%201%2C%203)%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%20%3C%3E%20''%2C%20dictGetString('dc'%2C%20'dc'%2C%20sipHash64(host))%2C%20'undefined_dc'%20)%20as%20dc%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        dc,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
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
#### <a id='6bd6982743d822f724a0fc0107a3cd76'></a>market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    host,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        host,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        host as host,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ddbd900b596e4263525301f2dc6544c8'></a>market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20host%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20host%20as%20host%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    host,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    host as host,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.host.splits.%24%7Bhost%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20host%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20host%20as%20host%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        host,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
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
#### <a id='489b6745f0553b48bd21c228e3cb5313'></a>market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    requester,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        requester,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
    GROUP BY metric_ts,
        multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='dddddd5d61cbf80670d9c2a32b3499f5'></a>market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
    requester,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')

GROUP BY metric_ts,
    multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.requester.splits.%24%7Brequester%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20extract(kv_values%5BindexOf(kv_keys%2C%20'userAgent')%5D%2C'Googlebot%7CGoogleDocs%7CGoogle-Ads-Creatives-Assistant%7CYaDirectBot%7CYaDirectFetcher%7CYandexRCA%7CYandexDirectDyn%7CYandexAccessibilityBot%7CMail.RU_Bot%7CBingPreview%7CMediapartners-Google%7CFeedfetcher-Google%3B%7CAdsBot-Google%7CYahoo!%20Slurp%7CWebAlta%7CStackRambler%7Cmsnbot%7Cbingbot%7CAport%7CMail%5C%5C.Ru%2F%7CYandex%2F%7CStatbox%2F%7CYandexSomething%2F%7CYandexBlog%2F%7CYandex%5C%5C.Server%2F%7CYaDirectBot%7CJakarta%20Commons-HttpClient%2F%7CTurtleScanner%7CNovoteka%7Cia_archiver%7Cheritrix%7CTwiceler-%7Cpsbot%2F%7CAlchemy%20Eye%20Agent%7CEchoping%2F%7CFriends%2F%7CWhatsUp%2F%7CWhatsUp_Gold%2F%7C%3B%20HttpSatPinger%5C%5C)%7CMSRBOT%20%5C%5C(http%3A%2F%2Fresearch%5C%5C.microsoft%5C%5C.com%2Fresearch%2Fsv%2Fmsrbot%2F%7CMJ12bot%2F%7Cichiro%2F%7CTECOMAC-Crawler%2F%7CGigabot%7CSogou%20Push%20Spider%7Ccheck_http%2F%7Chttp_ping%7CKeepAliveClient%7CSamSunf%7CGenHash%7CIRLbot%7CUptimeInspector%7Cliveinternet%20spider%7CBegun%20Robot%20Crawler%7CInternetSeer%5C%5C.com%7CRefer%5C%5C.Ru%20Favicon%20Bot%7CRobot%20Semonitor%7CRobot%20PagePromoter%7CSESpider%7CJakarta%20Commons-HttpClient%7CParasite%20Eliminator%7CSpinn3r%7CYandexBot%2F%7CYandexImages%2F%7CYandexVideo%2F%7CYandexMedia%2F%7CYandexBlogs%2F%7CYandexFavicons%2F%7CYandexAddurl%2F%7CYandexImageResizer%2F%7CYandexDirect%2F%7CYandexMetrika%2F%7CYandexNews%2F%7CYandexCatalog%2F%7CYandexWebmaster%2F')%20!%3D%20''%2C%20'robot'%2C%20yandex_login%20%3D%20''%2C%20'anonymous'%2C%20'logged-in'%20)%20as%20requester%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0,
        requester,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api')
    
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
#### <a id='9faa98411850298e3c3c1aeafc790b39'></a>market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0,
    page,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0,
        page,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')
    
    GROUP BY metric_ts,
        replaceAll(page_id, ':', '_') as page,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='54a255581963941e074cd7f856670454'></a>market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20page%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0,
    page,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')

GROUP BY metric_ts,
    replaceAll(page_id, ':', '_') as page,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.page.splits.%24%7Bpage%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20page_id%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%20as%20page%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0,
        page,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '')
    
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
#### <a id='094b1ea53d1d843e57fac45739a8cbea'></a>market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0,
    region,
    target_module,
    request_method

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.any-code.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0,
        region,
        target_module,
        request_method
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')
    
    GROUP BY metric_ts,
        replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
        coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
        coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2a218aaf66f4a002e1d6e037efaca8a1'></a>market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20region%2C%0A%20%20%20%20target_module%2C%0A%20%20%20%20request_method%2C%0A%20%20%20%20code%0A%0AFROM%20market.market_front_trace%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0,
    region,
    target_module,
    request_method,
    code

FROM market.market_front_trace

WHERE date = today() and timestamp > now() - 60 * 60
    AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')

GROUP BY metric_ts,
    replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region,
    coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module,
    coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method,
    concat(substring(toString(http_code),1,1),'xx') as code

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.trace.v3.white_fapi.region.splits.%24%7Bregion%7D.%24%7Btarget_module%7D.%24%7Brequest_method%7D.code.%24%7Bcode%7D.metrics.bytes_send.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesIf(0.5%2C0.7%2C0.9%2C0.95%2C0.97%2C0.99%2C0.995%2C1)(response_size_bytes%2Cenvironment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20region%2C%0A%20%20%20%20%20%20%20%20target_module%2C%0A%20%20%20%20%20%20%20%20request_method%2C%0A%20%20%20%20%20%20%20%20code%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_front_trace%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(environment%20%3D%20'PRODUCTION'%20and%20module%20%3D%20'market_front_touch_api'%20and%20region%20!%3D%20'')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values%5BindexOf(kv_keys%2C%20'regionId')%5D))%2C%20'en')%2C%20'%20'%2C%20'_')%20as%20region%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(target_module%2C%20'')%2C%20'UNKNOWN_SERVICE')%20as%20target_module%2C%0A%20%20%20%20%20%20%20%20coalesce(nullIf(request_method%2C%20'')%2C%20'UNKNOWN_METHOD')%20as%20request_method%2C%0A%20%20%20%20%20%20%20%20concat(substring(toString(http_code)%2C1%2C1)%2C'xx')%20as%20code%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0,
        region,
        target_module,
        request_method,
        code
    
    FROM market.market_front_trace
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '')
    
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
    SELECT 'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #3

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and error_code != '') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #4

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '' and error_code != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.error.any-error.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.error.split.${error}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, error FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '' and error_code != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, replaceRegexpAll(error_code,'[^a-zA-Z0-9]', '_') as error ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.rps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #5

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #6

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.ttlb.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(duration_ms,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_desktop.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_desktop' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #7

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_touch.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.total.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, dc, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.dc.splits.${dc}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, dc, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( substring(host, 1, 3) in ('iva', 'man', 'vla', 'sas', 'myt'), substring(host, 1, 3), endsWith(host, 'yp-c.yandex.net'), substring(host, position(host, '.') + 1, 3), dictGetString('dc', 'dc', sipHash64(host)) <> '', dictGetString('dc', 'dc', sipHash64(host)), 'undefined_dc' ) as dc, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, host, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.host.splits.${host}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, host, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, host as host, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, requester, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.requester.splits.${requester}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api') as value_0, requester, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api') GROUP BY metric_ts, multiIf( extract(kv_values[indexOf(kv_keys, 'userAgent')],'Googlebot|GoogleDocs|Google-Ads-Creatives-Assistant|YaDirectBot|YaDirectFetcher|YandexRCA|YandexDirectDyn|YandexAccessibilityBot|Mail.RU_Bot|BingPreview|Mediapartners-Google|Feedfetcher-Google;|AdsBot-Google|Yahoo! Slurp|WebAlta|StackRambler|msnbot|bingbot|Aport|Mail\\.Ru/|Yandex/|Statbox/|YandexSomething/|YandexBlog/|Yandex\\.Server/|YaDirectBot|Jakarta Commons-HttpClient/|TurtleScanner|Novoteka|ia_archiver|heritrix|Twiceler-|psbot/|Alchemy Eye Agent|Echoping/|Friends/|WhatsUp/|WhatsUp_Gold/|; HttpSatPinger\\)|MSRBOT \\(http://research\\.microsoft\\.com/research/sv/msrbot/|MJ12bot/|ichiro/|TECOMAC-Crawler/|Gigabot|Sogou Push Spider|check_http/|http_ping|KeepAliveClient|SamSunf|GenHash|IRLbot|UptimeInspector|liveinternet spider|Begun Robot Crawler|InternetSeer\\.com|Refer\\.Ru Favicon Bot|Robot Semonitor|Robot PagePromoter|SESpider|Jakarta Commons-HttpClient|Parasite Eliminator|Spinn3r|YandexBot/|YandexImages/|YandexVideo/|YandexMedia/|YandexBlogs/|YandexFavicons/|YandexAddurl/|YandexImageResizer/|YandexDirect/|YandexMetrika/|YandexNews/|YandexCatalog/|YandexWebmaster/') != '', 'robot', yandex_login = '', 'anonymous', 'logged-in' ) as requester, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #8

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0, page, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.page.splits.${page}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') as value_0, page, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and page_id != '') GROUP BY metric_ts, replaceAll(page_id, ':', '_') as page, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.any-code.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0, region, target_module, request_method FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.trace.v3.white_fapi.region.splits.${region}.${target_module}.${request_method}.code.${code}.metrics.bytes_send.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesIf(0.5,0.7,0.9,0.95,0.97,0.99,0.995,1)(response_size_bytes,environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') as value_0, region, target_module, request_method, code FROM market.market_front_trace WHERE date = today() and timestamp > now() - 60 * 60 AND (environment = 'PRODUCTION' and module = 'market_front_touch_api' and region != '') GROUP BY metric_ts, replaceAll(regionToName(regionToCountry(toUInt32OrZero(kv_values[indexOf(kv_keys, 'regionId')])), 'en'), ' ', '_') as region, coalesce(nullIf(target_module, ''), 'UNKNOWN_SERVICE') as target_module, coalesce(nullIf(request_method, ''), 'UNKNOWN_METHOD') as request_method, concat(substring(toString(http_code),1,1),'xx') as code ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

