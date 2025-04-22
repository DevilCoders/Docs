# market/market_client_timers/market_front_unified_blue_client_timers
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `market_client_timers`

## Splits

```json
{
    "service_blue": "multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' )",
    "page": "arrayJoin(['any-page', replaceAll(page_id, ':', '_')])",
    "buckets_ttr": "if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms)))",
    "buckets_tti": "if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms)))",
    "buckets_ttrStart": "if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]))))",
    "buckets_ttrEnd": "if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]))))",
    "buckets_ttrDuration": "if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]))))",
    "buckets_ttiStart": "if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]))))",
    "buckets_ttiEnd": "if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]))))",
    "buckets_ttiDuration": "if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]))))",
    "buckets_ttiShift": "if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]))))",
    "buckets_ttiRawStart": "if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]))))",
    "buckets_ttiRawEnd": "if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]))))",
    "buckets_ttiRawDuration": "if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]))))",
    "widget": "replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '')",
    "buckets_stuffing": "if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]))))",
    "buckets_hydrating": "if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]))))",
    "robotness": "if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans')",
    "requester": "if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in')",
    "regionName": "regionToName(regionToCountry(region), 'en')"
}
```

## Filters

```json
[
    "platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen'",
    "platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget'"
]
```

## Resulting metrics

  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps`](#f757e25d7a03cd685c68bcf2a6f0756a)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#baacd047d0eca8b122e07918a149a6c8)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles`](#4665b98f477669f31ebce46c1467d986)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#6d2d23770dac1a9ab07187ed00473b81)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles`](#86f63400301eca215422cd446ab46073)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#ae1bcab984ee32fcd7c1d6eb2cab3e5b)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#96e8fbc021e7a1a640928f55604739dc)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#217a8b0f110755125f52d9d178d9cd16)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#1d2dea1a7035415061e97dcf5de27164)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#0aada251dbbfb0ba0c07934a71b35b5c)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#822bb4ddd36a2c0d94c66ce3961e3c99)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#4ab15673eb2fda5aa83ff527b4b26884)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#6049821d99ff3af0d24a4ef6c967394a)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#b8e848b0e3055525964d69540aafc752)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#410a2e69e4205f6ca9b631b6b4a8f1cf)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#45fbf9ae2062ec8448e077838476e666)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#4ceeeaefb2b5da362ef20aa234b96915)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#d0111189233576ee1387388efd480e2b)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#973d54a449b132d54d4cfc0317c1c033)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#84af12fec9e3bfb1b04b46bb25f24cb0)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#0acd3e79d83a8f97cb15bce472471f1f)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#9c9dfcb66a11b537d754e5e559347e1a)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#f1715dfdb3786d9391a258b3ec0bda91)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#ea7636d99f0c7c9139a5305a2d243d47)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#fa818f1c412ec88426370dab9d697d7f)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps`](#317783959e30d8ccbfa0019dc4fc461e)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#c94b8f72a322140621df8a4303aca325)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#55513db75d2927f5310660d5bfbb2e3e)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#66f2133edaad24bfc55ce18329fde31d)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#0d6fb8e4626232047a1bcf37c9c87c9a)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.hps`](#1c69c568e3343652d76ac552a8b1feb5)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#b2f3931a695e36bbe453dc5912998f37)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles`](#6d6c4ca5beb0d3357e2316b594feda5c)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#1606394a123eb9ec0741a5634f1470c8)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles`](#c9880c1ad4babaea4f3ab3ce2b9bf90e)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#1e956fee349dd718849527b5e344631b)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#a861e1ee45489eef062cc8987bb7c2ea)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#d1b620064b3e0530dfdd93ca74d3c322)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#f24333f6bde432271b78329d5513712d)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#4d16e635f3b4566f4d3229096c13e1ce)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#e9c3c6b0adbab76c4edfc6279b0cf4f7)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#fee2e84eaeabeea1b228a1b516670cfa)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#aac0f949c13802edca9cc9e5e80c3699)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#267f8d7c5fbf6a49bd6f76d7643c1df3)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#2c30243c669fd0bb4bc902d34c0aab04)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#97d7cb1fcb3f7aaafae26f2be4c6db64)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#2c92f8cedf51a62d115615dd3729c1e8)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#695fe35231a07ec699bb75491a5aa3d2)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#cfc02fa599b77e1ee2de57594116d12f)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#c0552a0bde905fcaa627d15b8133ec29)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#3f5ec52f06686519c673b0abd6f06439)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#f0c885e49668dcb9838972faf95bf4fb)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#1678f5554bd9480346d8ccf4d1a61949)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#7772e94b2211ef94ac5f7cd89ccf9d3e)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#d081f070230fd923ff48d7f63998479d)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps`](#b8f86c668a680bf09552b62c9c43bb58)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#6e0a4e42d225ce423b8e2e425df37713)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#9e2d714cdfa1afa6a417709a32ccefa2)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#a70723399b65ece11c85234ffd5f83b0)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#4e131c24c47ecfcbedbce7ea7a1c9efc)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps`](#0d8471d8a1fcd269db1c3c5b1c09df3c)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#72aab556ac8d672c3ceec7cdbb0c7df2)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles`](#540a576486c1c18a406a9995eb2ffca3)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#5de5b65a331e9b4fe5a1ac2fc8cb6ef7)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles`](#0f2695b8dcb186c8d936353a975fe81d)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#e503d845b91fa0ba19f0301e4062078f)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#0b408806b0b6aae9e448fb8093798615)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#6e54ccca1b5eece73223044b887365cc)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#0074736d35e54da3c1bc327593c5bc57)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#3b8b5ab29cc5db6ca49fc0f12e12efdc)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#b86d7422496facd77895886c8dfec70e)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#e7d137e38d507d4e0aa108f85499eb0d)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#492eb0b2e65b6c285408d0f2d69ca4bd)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#9714dde44d8df4e03b176e03455def13)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#5c230edcc2f6021dce699c8da36ebccf)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#d7e29270065d10a95c492c5204fc3abf)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#40a2401f3f6e413936a22c8a59bf2476)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#23aa814ee99ceb56d5da47e51a40cd39)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#03c0dcd7108b4e019907e72d488870b0)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#2dec7bba33fb275ffee133c3bc7240e9)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#fd26edc9c7a95114bf96462dbd9295af)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#61a0720d378edd9f0cbc851ea578a495)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#85837c945c841f09f63cd23f8b559d2d)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#ec24247524ada8c653d06c2bfab05bc3)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#ccd317b7f229d6753cd8e4f2cfc3295f)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps`](#404c917e3b453a44a9281a2427513ab1)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#77dde591e3c79fa57c7fdf6036d3bd6b)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#4164e85fc091bf653dcef27e6af2f949)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#cb71e0dd8576ab9b67ef32eb162f6b7b)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#a84fca054dbbb5a25a749eaa42449c7a)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.hps`](#02b98645f9720d68d5f6200fd6017520)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#d2f7c50efcf80c9d17fca18ccff18211)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.tti.quantiles`](#343266ee00eebc956cf6aa0709198623)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#07ee4581134b6e00fe1f95dbfdfb3b0f)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.ttr.quantiles`](#9236e0cea8bddd78bed5723ce04453c0)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#772ab740a91258589dd57f1aa0252dc6)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#60dcb74a784574f067daf328d6bf24a3)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#36862f666b8c7edfef23825597087280)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#2dfe5b43e2a29f65e4d60ba77b9a3b45)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#5d1e1b8577d2459f2086f194c0cf8e4e)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#30a76b06c6a5edae29cfc270e2708efb)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#b55a06f44ab0034734cfcb3d2df80b89)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#8b0a3ec58b12a414082b5d2ec869d621)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#027670031422c6d0a4b1413b74665a9a)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#84549941f95f0464e7dbe9276133cb25)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#3ab8164364fe1515e3d850a565ab5d97)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#4b36d30d81e0c2dc3e630fdcd34ee204)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#26d527fdfc999e5a3c0d1651d221dc25)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#1b803adbee7521e88eae551bf4310da6)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#89aefc9f5ea565ca8972f5e6e89acb67)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#438430cf2aaf0175c248d9836d9ac764)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#5884ede3b2d4fe231fce2235c3d10434)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#b976ab2e21c3222ecfec4c94035ca592)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#bc8cd753e568a6463b8f0078d093980f)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#ff5cabb6c3b30d61dc2aacb3d61f2382)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hps`](#def8c9e8f171f8c4649841bb5818c6a9)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#80b123d8e1164a38d2e45b852d9bfe7c)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#ea716eedaf7d3ba9131c1bd3dffa31e1)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#97f85ca5dd08184cc7e67b5c7bca827a)
  * [`market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#fc5662635274a731e26619d8005e8ca2)

## Metrics

#### <a id='02b98645f9720d68d5f6200fd6017520'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='07ee4581134b6e00fe1f95dbfdfb3b0f'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d2f7c50efcf80c9d17fca18ccff18211'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bc8cd753e568a6463b8f0078d093980f'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5884ede3b2d4fe231fce2235c3d10434'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='89aefc9f5ea565ca8972f5e6e89acb67'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b55a06f44ab0034734cfcb3d2df80b89'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='36862f666b8c7edfef23825597087280'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='772ab740a91258589dd57f1aa0252dc6'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5d1e1b8577d2459f2086f194c0cf8e4e'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='26d527fdfc999e5a3c0d1651d221dc25'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3ab8164364fe1515e3d850a565ab5d97'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='027670031422c6d0a4b1413b74665a9a'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0d8471d8a1fcd269db1c3c5b1c09df3c'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5de5b65a331e9b4fe5a1ac2fc8cb6ef7'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='72aab556ac8d672c3ceec7cdbb0c7df2'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ec24247524ada8c653d06c2bfab05bc3'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='61a0720d378edd9f0cbc851ea578a495'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2dec7bba33fb275ffee133c3bc7240e9'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e7d137e38d507d4e0aa108f85499eb0d'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6e54ccca1b5eece73223044b887365cc'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e503d845b91fa0ba19f0301e4062078f'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3b8b5ab29cc5db6ca49fc0f12e12efdc'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='23aa814ee99ceb56d5da47e51a40cd39'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d7e29270065d10a95c492c5204fc3abf'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9714dde44d8df4e03b176e03455def13'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1c69c568e3343652d76ac552a8b1feb5'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1606394a123eb9ec0741a5634f1470c8'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b2f3931a695e36bbe453dc5912998f37'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7772e94b2211ef94ac5f7cd89ccf9d3e'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f0c885e49668dcb9838972faf95bf4fb'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c0552a0bde905fcaa627d15b8133ec29'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fee2e84eaeabeea1b228a1b516670cfa'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d1b620064b3e0530dfdd93ca74d3c322'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1e956fee349dd718849527b5e344631b'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4d16e635f3b4566f4d3229096c13e1ce'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='695fe35231a07ec699bb75491a5aa3d2'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='97d7cb1fcb3f7aaafae26f2be4c6db64'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='267f8d7c5fbf6a49bd6f76d7643c1df3'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f757e25d7a03cd685c68bcf2a6f0756a'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6d2d23770dac1a9ab07187ed00473b81'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='baacd047d0eca8b122e07918a149a6c8'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ea7636d99f0c7c9139a5305a2d243d47'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9c9dfcb66a11b537d754e5e559347e1a'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='84af12fec9e3bfb1b04b46bb25f24cb0'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4ab15673eb2fda5aa83ff527b4b26884'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='217a8b0f110755125f52d9d178d9cd16'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ae1bcab984ee32fcd7c1d6eb2cab3e5b'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0aada251dbbfb0ba0c07934a71b35b5c'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d0111189233576ee1387388efd480e2b'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='45fbf9ae2062ec8448e077838476e666'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b8e848b0e3055525964d69540aafc752'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='def8c9e8f171f8c4649841bb5818c6a9'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='97f85ca5dd08184cc7e67b5c7bca827a'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='80b123d8e1164a38d2e45b852d9bfe7c'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='404c917e3b453a44a9281a2427513ab1'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='cb71e0dd8576ab9b67ef32eb162f6b7b'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='77dde591e3c79fa57c7fdf6036d3bd6b'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    robotness,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        robotness,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b8f86c668a680bf09552b62c9c43bb58'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a70723399b65ece11c85234ffd5f83b0'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6e0a4e42d225ce423b8e2e425df37713'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    requester,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        requester,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='317783959e30d8ccbfa0019dc4fc461e'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='66f2133edaad24bfc55ce18329fde31d'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c94b8f72a322140621df8a4303aca325'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_blue,
    regionName,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_blue,
        regionName,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9236e0cea8bddd78bed5723ce04453c0'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0f2695b8dcb186c8d936353a975fe81d'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c9880c1ad4babaea4f3ab3ce2b9bf90e'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='86f63400301eca215422cd446ab46073'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='343266ee00eebc956cf6aa0709198623'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='540a576486c1c18a406a9995eb2ffca3'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6d6c4ca5beb0d3357e2316b594feda5c'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4665b98f477669f31ebce46c1467d986'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ff5cabb6c3b30d61dc2aacb3d61f2382'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ccd317b7f229d6753cd8e4f2cfc3295f'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d081f070230fd923ff48d7f63998479d'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fa818f1c412ec88426370dab9d697d7f'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b976ab2e21c3222ecfec4c94035ca592'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='85837c945c841f09f63cd23f8b559d2d'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1678f5554bd9480346d8ccf4d1a61949'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f1715dfdb3786d9391a258b3ec0bda91'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='438430cf2aaf0175c248d9836d9ac764'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fd26edc9c7a95114bf96462dbd9295af'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3f5ec52f06686519c673b0abd6f06439'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0acd3e79d83a8f97cb15bce472471f1f'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8b0a3ec58b12a414082b5d2ec869d621'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='492eb0b2e65b6c285408d0f2d69ca4bd'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='aac0f949c13802edca9cc9e5e80c3699'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6049821d99ff3af0d24a4ef6c967394a'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2dfe5b43e2a29f65e4d60ba77b9a3b45'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0074736d35e54da3c1bc327593c5bc57'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f24333f6bde432271b78329d5513712d'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1d2dea1a7035415061e97dcf5de27164'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='60dcb74a784574f067daf328d6bf24a3'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0b408806b0b6aae9e448fb8093798615'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a861e1ee45489eef062cc8987bb7c2ea'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='96e8fbc021e7a1a640928f55604739dc'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='30a76b06c6a5edae29cfc270e2708efb'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b86d7422496facd77895886c8dfec70e'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e9c3c6b0adbab76c4edfc6279b0cf4f7'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='822bb4ddd36a2c0d94c66ce3961e3c99'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1b803adbee7521e88eae551bf4310da6'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='03c0dcd7108b4e019907e72d488870b0'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='cfc02fa599b77e1ee2de57594116d12f'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='973d54a449b132d54d4cfc0317c1c033'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4b36d30d81e0c2dc3e630fdcd34ee204'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='40a2401f3f6e413936a22c8a59bf2476'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2c92f8cedf51a62d115615dd3729c1e8'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4ceeeaefb2b5da362ef20aa234b96915'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='84549941f95f0464e7dbe9276133cb25'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5c230edcc2f6021dce699c8da36ebccf'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2c30243c669fd0bb4bc902d34c0aab04'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='410a2e69e4205f6ca9b631b6b4a8f1cf'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_blue,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_blue,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fc5662635274a731e26619d8005e8ca2'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
    service_blue,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
        service_blue,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a84fca054dbbb5a25a749eaa42449c7a'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
    service_blue,
    robotness,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
        service_blue,
        robotness,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4e131c24c47ecfcbedbce7ea7a1c9efc'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
    service_blue,
    requester,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
        service_blue,
        requester,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0d6fb8e4626232047a1bcf37c9c87c9a'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
    service_blue,
    regionName,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
        service_blue,
        regionName,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ea716eedaf7d3ba9131c1bd3dffa31e1'></a>market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
    service_blue,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
        service_blue,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4164e85fc091bf653dcef27e6af2f949'></a>market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
    service_blue,
    robotness,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
        service_blue,
        robotness,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9e2d714cdfa1afa6a417709a32ccefa2'></a>market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
    service_blue,
    requester,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
        service_blue,
        requester,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='55513db75d2927f5310660d5bfbb2e3e'></a>market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_blue%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
    service_blue,
    regionName,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_blue%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20%3D%20225%20and%20service_blue%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('beru.ru'%2C'pokupki.market.yandex.ru')%2C%20'blue_desktop'%2Cvhost%20in%20('m.beru.ru'%2C'm.pokupki.market.yandex.ru')%2C%20'blue_touch'%20%2C%20'undefined_service'%20)%20as%20service_blue%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0,
        service_blue,
        regionName,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```


## Overall Diagnostics

### Portion #1

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #3

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, robotness, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #4

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, requester, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_blue, regionName, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #5

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #6

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') as value_0, service_blue, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0, service_blue, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0, service_blue, robotness, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0, service_blue, requester, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0, service_blue, regionName, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0, service_blue, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0, service_blue, robotness, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0, service_blue, requester, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_blue}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') as value_0, service_blue, regionName, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) = 225 and service_blue != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('beru.ru','pokupki.market.yandex.ru'), 'blue_desktop',vhost in ('m.beru.ru','m.pokupki.market.yandex.ru'), 'blue_touch' , 'undefined_service' ) as service_blue, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

