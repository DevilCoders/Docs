# market/market_client_timers/market_front_unified_black_client_timers
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `market_client_timers`

## Splits

```json
{
    "service_black": "multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' )",
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
    "platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen'",
    "platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget'"
]
```

## Resulting metrics

  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps`](#128729cd960e5c1506d6fe66f213af0e)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#2a9936d50118b7fabbb300328e68b733)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles`](#95f98dfd2089c5e733e92cb8240fe4e8)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#1460e9cbf96c5ecb6ed5a17020ce1630)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles`](#db7eb62b3bd51a64321ccb7fe2bb920b)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#7237b177f9212901e7f669b2b66fd5b3)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#f65a88173219aa8e6cef3377daa59ede)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#05693f6e58c89ac01da0680c822d51d1)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#7a3f42d9cb1c1372326aedeab0f5e2c1)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#325fbfa7fc2e523626261b6a04c70983)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#186b9734b53b69d3e312cd47ee28cb4c)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#d82faa4b37a36892502a97a8d62f10e8)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#a6710fe5ebc5e3d1cc1c5ee40ee2dc3e)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#402e5e56566ca611efee5ff5377cf6c5)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#8d00fea42b0f416ccd8ac74e28687b01)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#136d452269a519587f554389b83d48d7)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#28cc3614ca5116e42e7d36f42e98f737)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#320b21785a69c4f1e2d946680bc792f9)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#591274c10167a77fdc99a56900b915c4)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#aad2bf2830c775dbb12fcafdc623ff0b)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#d5cb49c58ea0937978747209308c0af2)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#86e29c731ee33ac7c0b36a506a13ea0c)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#c681d091c0f79f40edb45eb952f8fc34)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#fb521cc28e74d12a217de647503670bb)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#2302a3878e1172d769df2d9803e83714)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps`](#8eb67086d8d1ceb20787a036233ad796)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#1fcf1d47faa77819f51865d1fb4a36fd)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#05c9e1b737ee42b70c3a21a3b29c926c)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#c0f8328458df5a062f357e5d5c7bfaed)
  * [`market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#197cca614ef0e542398211ad457adc0e)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.hps`](#c1e665a13c69502de9ebcfe9b53df52f)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#51497c3e8114d6afba3489d4a9dfbe51)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles`](#0d9e6ed0224342acd8fb3741124cc0a4)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#b68108bec7b5cac2459021f9173eb2d8)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles`](#e06614de709e203e6abee6ab65172532)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#18da6315b37b465f6464e5cdb33fb5ff)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#21cf10c98467e6b4416fdd9b8a0ad6f2)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#e110400fddd0cb3b89b68ff6311e7e0c)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#a58124cb5226e88ab6cd68fb297d40e6)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#33062861002e0f55dda5ec08a901b46d)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#c71d3a863dc286e0f077c673ad66c0fc)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#e5a12b7810aa70f135b979fea9af4cc0)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#f547741bc67de2e2d3eb8da7afff2efb)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#f7669154d4c199df2cdaeed584373016)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#f1e82776d2e0d4dc900ea493d41f652e)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#65173d1faec1c4e902ecb5a2a81ec2cd)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#42f158983be0d29e0d64c9588709675a)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#c70819a70910deadd5c2e1babb8e8d29)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#036f1592ff362c5d64c221fb97225226)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#54f90aff73ff900f679f699945ca7c4d)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#174e678aeffb7bd80de0e9ee52385d12)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#0ae5e536959120a70067df5485a41805)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#665ee68fb3d512e53df7456992a799c2)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#756c2c958b09c4b556013fd79ac8134c)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#67fa996dcc1b83d5ab5baded1c80edb7)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps`](#5bd458549bfa651ec0e3343df8f55b90)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#8eee39c40d42a63d993967758e83f42e)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#fe6c64d1110b4cfad4131e6d337722dd)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#5cc83fe8c664e1f60251e302463ca00c)
  * [`market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#838defef1fd056bc58f1a4e59c15dee5)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps`](#6edfe76057fb1e8964c7824239e24da7)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#3ecdfe6dfd0a661e4a49007f7b366766)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles`](#d5a14c00fda6e937da387dd8efd07c00)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#abdb2cc685cde83d000d7dbb7358f4a8)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles`](#20b4c22de998ac1756750d6483bacc92)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#606fd31cb1694e8e9438643950611f24)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#3dbf99789ad3381924eb2181138f64c9)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#a2eb6b1717dd27fb382c4aa2d15d66d0)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#dacbd473ecc00faa0354e40f0213fa83)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#b24c78745566a90f84dc43c7a10312d4)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#6b932329500c8d39882f1eb319204e33)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#e6f3aba260128156c5d59a5ebe2f5f38)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#4566023d0c28d1053ce4efc53a28f2e9)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#aa3b4e8480356b25c30cba50f86ddb34)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#3a83cfaa3c4678d2c9b7494e750cc218)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#e568f85c75b1c8de85cfffcea30e2c3a)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#d57cd868a32948b3b4d283338c67fc7d)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#d717a4d3e4d86bd6d2ad9114dbed8fed)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#55e3ac638e62d447f5729d6fab6ace1b)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#0069e4bb93731f0b9c120d31e8d64692)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#f0b38191d8b73c78023b87e332082fd6)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#9c73bee115b01fa61515549c731b1a64)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#26b323baf78853fe6d2213a8ac581fe7)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#1021fa300162e1295fcf410661d9f65c)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#51baa90c179c1d2d5f0b05a91bbb441d)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps`](#743736c9e12103ed4f965d4ad3ccb467)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#74f41e911455afe9bdda9678b61f09e2)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#99d625024aa44ef9128754bffc494c71)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#216de42ef3a48deba86181cb1a0288fd)
  * [`market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#a1f59ceb6ed4db0b98b750f233e98c11)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.hps`](#fd031246a6057c77af132ae827f5bbe0)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#95bd9089339e3ec74007c1fd0234649e)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.tti.quantiles`](#0ec5ca9dee76178e3215fc8fd4367694)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#89a82e8d28c3a96616f7d017c3333539)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.ttr.quantiles`](#47ccf7765657aa9aaed4a2aa18efeac6)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#8fa42803d03ce5488ef215f2067f2d86)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#dc9ea95c3acd548794d1712ceda6be44)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#b3a579d7d6f823c2f19888167f68f2f1)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#d31d000118aa2ff1d9f5f787b94cf7c7)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#4836be46b25151b5dfda91e479955aff)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#4d6e3c4b823a6a997e676017beb54b62)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#1137ee6b6d120816fe9d6a5dcf9d1513)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#cd680847f52c0bf3104db0a08a30cca3)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#d816acaac374eecda662eba27fade296)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#3c9087b16280dec5ba94a5680cfb5491)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#75cb63db622f4c0a11973d4f0d705583)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#0d7179f3c6845e89c2fa28f7e7284813)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#696a8961041e361db65b9c2837c2407c)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#92f4fecebe47708d27374f938b26bdda)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#2d67a79b442061c4cdf03f854b3e19fa)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#12110375150e119b7962c6079732d71d)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#9f552b635ebeb97adaf815056d5cd38a)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#44dd23609ca45f15c6725e03d3e6bdb6)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#2db8c65a3ad3c347b7c4f242874812be)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#9d4c3ce5feede1fbb2dc0c9a296ed56d)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hps`](#300f302f614121f981a1fe937de2c522)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#1257a9cb6ede171bf1a25c95ca8ee2fc)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#63e1279ef27cc35212aec958ae18cb2b)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#4f4cce28c15294c520c3708634460829)
  * [`market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#7eddda6e7403b769b5d6b7dddc3abb2d)

## Metrics

#### <a id='fd031246a6057c77af132ae827f5bbe0'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='89a82e8d28c3a96616f7d017c3333539'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='95bd9089339e3ec74007c1fd0234649e'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2db8c65a3ad3c347b7c4f242874812be'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9f552b635ebeb97adaf815056d5cd38a'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2d67a79b442061c4cdf03f854b3e19fa'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1137ee6b6d120816fe9d6a5dcf9d1513'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b3a579d7d6f823c2f19888167f68f2f1'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8fa42803d03ce5488ef215f2067f2d86'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4836be46b25151b5dfda91e479955aff'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='696a8961041e361db65b9c2837c2407c'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='75cb63db622f4c0a11973d4f0d705583'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d816acaac374eecda662eba27fade296'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6edfe76057fb1e8964c7824239e24da7'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='abdb2cc685cde83d000d7dbb7358f4a8'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3ecdfe6dfd0a661e4a49007f7b366766'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1021fa300162e1295fcf410661d9f65c'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9c73bee115b01fa61515549c731b1a64'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0069e4bb93731f0b9c120d31e8d64692'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e6f3aba260128156c5d59a5ebe2f5f38'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a2eb6b1717dd27fb382c4aa2d15d66d0'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='606fd31cb1694e8e9438643950611f24'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b24c78745566a90f84dc43c7a10312d4'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d717a4d3e4d86bd6d2ad9114dbed8fed'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e568f85c75b1c8de85cfffcea30e2c3a'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='aa3b4e8480356b25c30cba50f86ddb34'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c1e665a13c69502de9ebcfe9b53df52f'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b68108bec7b5cac2459021f9173eb2d8'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='51497c3e8114d6afba3489d4a9dfbe51'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='756c2c958b09c4b556013fd79ac8134c'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0ae5e536959120a70067df5485a41805'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='54f90aff73ff900f679f699945ca7c4d'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e5a12b7810aa70f135b979fea9af4cc0'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e110400fddd0cb3b89b68ff6311e7e0c'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='18da6315b37b465f6464e5cdb33fb5ff'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='33062861002e0f55dda5ec08a901b46d'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c70819a70910deadd5c2e1babb8e8d29'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='65173d1faec1c4e902ecb5a2a81ec2cd'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f7669154d4c199df2cdaeed584373016'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='128729cd960e5c1506d6fe66f213af0e'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1460e9cbf96c5ecb6ed5a17020ce1630'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2a9936d50118b7fabbb300328e68b733'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fb521cc28e74d12a217de647503670bb'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='86e29c731ee33ac7c0b36a506a13ea0c'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='aad2bf2830c775dbb12fcafdc623ff0b'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d82faa4b37a36892502a97a8d62f10e8'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='05693f6e58c89ac01da0680c822d51d1'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7237b177f9212901e7f669b2b66fd5b3'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='325fbfa7fc2e523626261b6a04c70983'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='320b21785a69c4f1e2d946680bc792f9'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='136d452269a519587f554389b83d48d7'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='402e5e56566ca611efee5ff5377cf6c5'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='300f302f614121f981a1fe937de2c522'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4f4cce28c15294c520c3708634460829'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1257a9cb6ede171bf1a25c95ca8ee2fc'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='743736c9e12103ed4f965d4ad3ccb467'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='216de42ef3a48deba86181cb1a0288fd'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='74f41e911455afe9bdda9678b61f09e2'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    robotness,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        robotness,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5bd458549bfa651ec0e3343df8f55b90'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5cc83fe8c664e1f60251e302463ca00c'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8eee39c40d42a63d993967758e83f42e'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    requester,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        requester,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8eb67086d8d1ceb20787a036233ad796'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c0f8328458df5a062f357e5d5c7bfaed'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1fcf1d47faa77819f51865d1fb4a36fd'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_black,
    regionName,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_black,
        regionName,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='47ccf7765657aa9aaed4a2aa18efeac6'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='20b4c22de998ac1756750d6483bacc92'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e06614de709e203e6abee6ab65172532'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='db7eb62b3bd51a64321ccb7fe2bb920b'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0ec5ca9dee76178e3215fc8fd4367694'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d5a14c00fda6e937da387dd8efd07c00'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0d9e6ed0224342acd8fb3741124cc0a4'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='95f98dfd2089c5e733e92cb8240fe4e8'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9d4c3ce5feede1fbb2dc0c9a296ed56d'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='51baa90c179c1d2d5f0b05a91bbb441d'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='67fa996dcc1b83d5ab5baded1c80edb7'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='2302a3878e1172d769df2d9803e83714'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='44dd23609ca45f15c6725e03d3e6bdb6'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='26b323baf78853fe6d2213a8ac581fe7'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='665ee68fb3d512e53df7456992a799c2'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c681d091c0f79f40edb45eb952f8fc34'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='12110375150e119b7962c6079732d71d'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f0b38191d8b73c78023b87e332082fd6'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='174e678aeffb7bd80de0e9ee52385d12'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d5cb49c58ea0937978747209308c0af2'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='cd680847f52c0bf3104db0a08a30cca3'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4566023d0c28d1053ce4efc53a28f2e9'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f547741bc67de2e2d3eb8da7afff2efb'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a6710fe5ebc5e3d1cc1c5ee40ee2dc3e'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d31d000118aa2ff1d9f5f787b94cf7c7'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='dacbd473ecc00faa0354e40f0213fa83'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a58124cb5226e88ab6cd68fb297d40e6'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7a3f42d9cb1c1372326aedeab0f5e2c1'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='dc9ea95c3acd548794d1712ceda6be44'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3dbf99789ad3381924eb2181138f64c9'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='21cf10c98467e6b4416fdd9b8a0ad6f2'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f65a88173219aa8e6cef3377daa59ede'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4d6e3c4b823a6a997e676017beb54b62'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6b932329500c8d39882f1eb319204e33'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c71d3a863dc286e0f077c673ad66c0fc'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='186b9734b53b69d3e312cd47ee28cb4c'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='92f4fecebe47708d27374f938b26bdda'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='55e3ac638e62d447f5729d6fab6ace1b'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='036f1592ff362c5d64c221fb97225226'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='591274c10167a77fdc99a56900b915c4'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0d7179f3c6845e89c2fa28f7e7284813'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d57cd868a32948b3b4d283338c67fc7d'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='42f158983be0d29e0d64c9588709675a'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='28cc3614ca5116e42e7d36f42e98f737'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3c9087b16280dec5ba94a5680cfb5491'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3a83cfaa3c4678d2c9b7494e750cc218'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f1e82776d2e0d4dc900ea493d41f652e'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8d00fea42b0f416ccd8ac74e28687b01'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_black,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_black,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7eddda6e7403b769b5d6b7dddc3abb2d'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
    service_black,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
        service_black,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a1f59ceb6ed4db0b98b750f233e98c11'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
    service_black,
    robotness,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
        service_black,
        robotness,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='838defef1fd056bc58f1a4e59c15dee5'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
    service_black,
    requester,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
        service_black,
        requester,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='197cca614ef0e542398211ad457adc0e'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
    service_black,
    regionName,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
        service_black,
        regionName,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='63e1279ef27cc35212aec958ae18cb2b'></a>market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
    service_black,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
        service_black,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='99d625024aa44ef9128754bffc494c71'></a>market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
    service_black,
    robotness,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
        service_black,
        robotness,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fe6c64d1110b4cfad4131e6d337722dd'></a>market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
    service_black,
    requester,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
        service_black,
        requester,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='05c9e1b737ee42b70c3a21a3b29c926c'></a>market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_black%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
    service_black,
    regionName,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_black%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_black%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_black%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20%3D%20'business.market.yandex.ru'%2C%20'black_desktop'%20%2C%20'undefined_service'%20)%20as%20service_black%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0,
        service_black,
        regionName,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black,
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
    SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #3

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, robotness, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #4

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, requester, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_black, regionName, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #5

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #6

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') as value_0, service_black, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0, service_black, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0, service_black, robotness, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0, service_black, requester, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0, service_black, regionName, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0, service_black, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0, service_black, robotness, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0, service_black, requester, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_black}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') as value_0, service_black, regionName, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_black != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost = 'business.market.yandex.ru', 'black_desktop' , 'undefined_service' ) as service_black, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

