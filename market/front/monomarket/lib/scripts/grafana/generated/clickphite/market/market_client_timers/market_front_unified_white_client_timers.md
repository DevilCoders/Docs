# market/market_client_timers/market_front_unified_white_client_timers
    
## Common properties

  * **Owner:** `marketfrontend`
  * **Table:** `market_client_timers`

## Splits

```json
{
    "service_white": "multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' )",
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
    "platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen'",
    "platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget'"
]
```

## Resulting metrics

  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps`](#1384d852abee4b7fe333d8e137edf420)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#6417d2e03ca5f0925d72858eef2ad902)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles`](#fca22664af724664910576225a812439)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#117f07623f9edf04f4fb5376c3921586)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles`](#bf53b5d85a12d80c0d399e26c8ad431d)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#478af8132efea69a7b8ae3784e0436e2)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#ae5d448602917a5f79dc864168130de0)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#34af0417d99e1e10bf1699030cf93459)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#1306f489aaad6d35c27d3acead962c0d)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#f3b0412e3e30e1eaa9338e998b75b4ab)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#dba69a61ba05e8dde57e60622922caac)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#88e1a7e0f16092e5def27f229902c8b4)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#61251b061f20752b315d13527835cd08)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#8433d49a2f55a1d61dc686af626307f9)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#ab71582a368dce6d85778a271850d08f)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#954a0997850e4db673464a513adb2fec)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#704ca800e7d6b75203201150460d3775)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#6c9ffd2573a46aaea7cc62b40a6acc06)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#f9754400cbd108cd61e44b63ed140ce4)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#b2a2d76f2f224cc653e8ffc93711d9a2)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#9ebadd98ff52a53c5fe5c628eb8fa29c)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#ac98d8cea2d0ff2ed057a66a0e72ed3e)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#efcabdd1565fcc5c0221ad16aeb1d686)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#a61800aa04f2580b4a594ce08496a4a6)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#28307d72410c80d928f68eeba2366526)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps`](#596fa7a0fdcd49ca7e72b0315c39d779)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#c7afbb941ba60b1da23622190681b9e5)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#bd14c8562b026e38c9e41ae00537297d)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#bfd64252c895cdc2689d56a38e58fe08)
  * [`market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#0b55059fec54baf894d2763f972d1649)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.hps`](#d0c8085519261d161fdb8f51b676a80d)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#836c2c30ce7a23e9ab3f85459c11aaeb)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles`](#9f52a8d3cb1f77973c6216ef8eda69f2)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#d7738089583cd7e0668ca43cb62af622)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles`](#cbb741be609e9d03cb4db9932080064c)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#c2468a4df6a75c21337629b24dd778ad)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#bfd949afabb81b26743918883fabd134)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#6b1b3661d112faf120504b76c0a62816)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#a40fc7f04879cc74d8896966f833579c)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#230bcc90f728b183f9b9aa921bf8ca7d)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#3a7afd785e304ecd0f557e99f6fd1496)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#5dd9e4fbd21c1bb50df5e78b26b23a7b)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#e5d8b53e2d47fdd6b5abe998c8e54d3d)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#6d89451c1b48f8d6474639f7c8db2f9d)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#9d38b248245f1d60c86cb9ea2bc3f6fd)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#28066238f5f4125826b822df683bf648)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#b1241189a7f182f408993e7e71a0407e)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#5981e7fe1628774babad697bb6e03a53)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#52f7c9692fc0df0832c3b599c2025d7a)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#d1e4f2d0a497e3530a6d9460e16f37b4)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#a932400589ba2dadf58839d894c77fa2)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#1ee75f30366aa46e0930b9f732f09d73)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#11c8b08685372f70319aed9bbb56ab12)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#c4a52708b0de2f6167d89155e449285b)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#e2b5c523bfcfc00a62eef2d6ea3f94ad)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps`](#11f932d911797795df1777d141cff836)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#a737f8381ad19dc42673c279244ed2b7)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#ef9635923716e13969d19410c161a512)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#3e43c951712132b327f8e3ec5c712ec0)
  * [`market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#8eb9744ffe4f0afd5766512cacac46e0)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps`](#f1d92e47dd7ce88ae7d450691742aefc)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#4ccc35c012ff3b14ddf57a3e0e06500c)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles`](#bbde39984238cf1bf18ec68299554106)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#c188d4d9cfbd3c1e3c01167a48ddd753)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles`](#a434d8f8d7cb929b8c83b57a6e2b10f1)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#061b6d2703614d39e25730629dce66fa)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#b0606d008b8784bc7475efffb4966f2a)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#3520aa1364ce11d8ff0aa31efafca1ef)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#37a20b544a1dd889503985cc7675b66f)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#48413bfb66124881d074421a309ee239)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#76025957f64dc0484dc83e67947fcaf5)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#9259670ef7ee175b31c41e30c4563312)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#49656525da1065c5e0c389f4a9ae531b)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#920e5775092b4083a95b7771b9d03f51)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#5a11a5241ac51874c4d2f5f6c80716df)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#1f0f237e876d7ce7cfeb717ddbd0956a)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#29caab2e2915b747539aa4517e6277bf)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#b5170b68ae669d71417e232f10655ea5)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#6e47d874217868247f12283892c7e80a)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#f946575e1c61195ecac2f7872601ad1d)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#407be5aee265f4a91e286331496aa147)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#7c6e49b0dc72d7040973665a010a0edb)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#57f67d43d65b22b5ffc4be14ec9126a3)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#bc469ed4a3a959ed633f85536e8cf431)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#1552ece62bc68c32b27320cbeed0b4df)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps`](#f1dd2beda65e99f81b9d00cc34719a91)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#47002ae2b79b59f28a03316a3ed3fecd)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#613f5dedaf574ed323ced7599d0600c5)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#0a924fa3da62b0fdcf10a92dd2757eba)
  * [`market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#c8a23b69f8274e12b32f2c61e24d7992)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.hps`](#d5969cd500fe7bcc699f6cc5e3cd330a)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}`](#17c8bf56e68bdca62b3058f378af1f41)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.tti.quantiles`](#3f4abf6ecc24b87f92bb3a4b3215031d)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}`](#cfb3508be0c86a2df6343156914f2d9c)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.ttr.quantiles`](#051df4948e768e284afc128ebbd28035)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}`](#b0ede562119a3ba09365cf3f252beeac)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles`](#4287e229aba84947c23fa55bc66bbac2)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}`](#0da58ab14e1c1d637cef1d3ca6f0eaa6)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles`](#41efa9a9a85f81dfaa5255a47b5b7e9c)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}`](#179227495223f56c2b05eddb5833c893)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles`](#513c852098f4cd75d8e6815371648310)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}`](#97a3bd44e65788463d383e19e75955fe)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles`](#6f7806d6612522c4fc9a09643050a3d7)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}`](#1830c2579f47aa1d2a5491b8a990fd60)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles`](#30f22299bb1ac480269733d34d76db98)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}`](#954a549721db327205acf7376a0e570e)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles`](#b9dd4f8db7e7083d8bf36fdb2a3aafd4)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}`](#cea49093317d5f4feb30d52f91fdfb4d)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles`](#5ff79cce799ec7bc94a8da2d3ebc3fe3)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}`](#25fcb1b100c7888d95f6fe61b117cb84)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles`](#d660dd0856a510dd53b4126ee6ffae4b)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}`](#ab2605cb7c505acd2f359ded07972936)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles`](#0dea8074115055e6bada1b25f19e5f89)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}`](#978a1f7f044677eced7661fde4613a6a)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles`](#95d2e950f95bc0011b61f2a1dec73238)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hps`](#6db68ac2b12b7d1b0626c1516e02f4b2)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}`](#da8533d71efe7fa10ac4777e54a5cfc6)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles`](#1fbe08f15b8f272cdb0e484b2cf013bd)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}`](#db0e0803b62b713eb0d08063bf7f2cf4)
  * [`market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles`](#ed6b05aea3e4abeced4cf3c4fb25d56a)

## Metrics

#### <a id='d5969cd500fe7bcc699f6cc5e3cd330a'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='cfb3508be0c86a2df6343156914f2d9c'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='17c8bf56e68bdca62b3058f378af1f41'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='978a1f7f044677eced7661fde4613a6a'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ab2605cb7c505acd2f359ded07972936'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='25fcb1b100c7888d95f6fe61b117cb84'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='97a3bd44e65788463d383e19e75955fe'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0da58ab14e1c1d637cef1d3ca6f0eaa6'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b0ede562119a3ba09365cf3f252beeac'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='179227495223f56c2b05eddb5833c893'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='cea49093317d5f4feb30d52f91fdfb4d'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='954a549721db327205acf7376a0e570e'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1830c2579f47aa1d2a5491b8a990fd60'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f1d92e47dd7ce88ae7d450691742aefc'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c188d4d9cfbd3c1e3c01167a48ddd753'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4ccc35c012ff3b14ddf57a3e0e06500c'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bc469ed4a3a959ed633f85536e8cf431'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='7c6e49b0dc72d7040973665a010a0edb'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f946575e1c61195ecac2f7872601ad1d'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9259670ef7ee175b31c41e30c4563312'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3520aa1364ce11d8ff0aa31efafca1ef'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='061b6d2703614d39e25730629dce66fa'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='48413bfb66124881d074421a309ee239'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b5170b68ae669d71417e232f10655ea5'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1f0f237e876d7ce7cfeb717ddbd0956a'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='920e5775092b4083a95b7771b9d03f51'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d0c8085519261d161fdb8f51b676a80d'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d7738089583cd7e0668ca43cb62af622'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='836c2c30ce7a23e9ab3f85459c11aaeb'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c4a52708b0de2f6167d89155e449285b'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1ee75f30366aa46e0930b9f732f09d73'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d1e4f2d0a497e3530a6d9460e16f37b4'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5dd9e4fbd21c1bb50df5e78b26b23a7b'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6b1b3661d112faf120504b76c0a62816'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c2468a4df6a75c21337629b24dd778ad'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='230bcc90f728b183f9b9aa921bf8ca7d'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5981e7fe1628774babad697bb6e03a53'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='28066238f5f4125826b822df683bf648'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6d89451c1b48f8d6474639f7c8db2f9d'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1384d852abee4b7fe333d8e137edf420'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='117f07623f9edf04f4fb5376c3921586'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttr%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_ttr

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.buckets.%24%7Bbuckets_ttr%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttr%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms)))%20as%20buckets_ttr%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_ttr
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6417d2e03ca5f0925d72858eef2ad902'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_tti%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_tti

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.buckets.%24%7Bbuckets_tti%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_tti%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms)))%20as%20buckets_tti%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_tti
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a61800aa04f2580b4a594ce08496a4a6'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_ttrStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.buckets.%24%7Bbuckets_ttrStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D))))%20as%20buckets_ttrStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_ttrStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ac98d8cea2d0ff2ed057a66a0e72ed3e'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_ttrEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.buckets.%24%7Bbuckets_ttrEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D))))%20as%20buckets_ttrEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_ttrEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b2a2d76f2f224cc653e8ffc93711d9a2'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttrDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_ttrDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.buckets.%24%7Bbuckets_ttrDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttrDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D))))%20as%20buckets_ttrDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_ttrDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='88e1a7e0f16092e5def27f229902c8b4'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_ttiStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.buckets.%24%7Bbuckets_ttiStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D))))%20as%20buckets_ttiStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_ttiStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='34af0417d99e1e10bf1699030cf93459'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_ttiEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.buckets.%24%7Bbuckets_ttiEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D))))%20as%20buckets_ttiEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_ttiEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='478af8132efea69a7b8ae3784e0436e2'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_ttiDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.buckets.%24%7Bbuckets_ttiDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D))))%20as%20buckets_ttiDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_ttiDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f3b0412e3e30e1eaa9338e998b75b4ab'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiShift%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_ttiShift

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.buckets.%24%7Bbuckets_ttiShift%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiShift%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D))))%20as%20buckets_ttiShift%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_ttiShift
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6c9ffd2573a46aaea7cc62b40a6acc06'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawStart%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_ttiRawStart

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.buckets.%24%7Bbuckets_ttiRawStart%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawStart%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D))))%20as%20buckets_ttiRawStart%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_ttiRawStart
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='954a0997850e4db673464a513adb2fec'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawEnd%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_ttiRawEnd

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.buckets.%24%7Bbuckets_ttiRawEnd%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawEnd%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D))))%20as%20buckets_ttiRawEnd%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_ttiRawEnd
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8433d49a2f55a1d61dc686af626307f9'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20buckets_ttiRawDuration%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    buckets_ttiRawDuration

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.buckets.%24%7Bbuckets_ttiRawDuration%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20buckets_ttiRawDuration%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D))))%20as%20buckets_ttiRawDuration%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        buckets_ttiRawDuration
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6db68ac2b12b7d1b0626c1516e02f4b2'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='db0e0803b62b713eb0d08063bf7f2cf4'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='da8533d71efe7fa10ac4777e54a5cfc6'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f1dd2beda65e99f81b9d00cc34719a91'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0a924fa3da62b0fdcf10a92dd2757eba'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='47002ae2b79b59f28a03316a3ed3fecd'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    robotness,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        robotness,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='11f932d911797795df1777d141cff836'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3e43c951712132b327f8e3ec5c712ec0'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a737f8381ad19dc42673c279244ed2b7'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    requester,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        requester,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='596fa7a0fdcd49ca7e72b0315c39d779'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hps'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bfd64252c895cdc2689d56a38e58fe08'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_stuffing%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    widget,
    buckets_stuffing

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.buckets.%24%7Bbuckets_stuffing%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_stuffing%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D))))%20as%20buckets_stuffing%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        widget,
        buckets_stuffing
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c7afbb941ba60b1da23622190681b9e5'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%2C%0A%20%20%20%20buckets_hydrating%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    count() / 60 as value_0,
    service_white,
    regionName,
    page,
    widget,
    buckets_hydrating

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
    if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.buckets.%24%7Bbuckets_hydrating%7D'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20count()%20%2F%2060%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%2C%0A%20%20%20%20%20%20%20%20buckets_hydrating%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%2C%0A%20%20%20%20%20%20%20%20if(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))%20%3E%2032000%2C%20'more_32000'%2C%20toString(roundToExp2(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D))))%20as%20buckets_hydrating%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        count() / 60 as value_0,
        service_white,
        regionName,
        page,
        widget,
        buckets_hydrating
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget,
        if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='051df4948e768e284afc128ebbd28035'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a434d8f8d7cb929b8c83b57a6e2b10f1'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='cbb741be609e9d03cb4db9932080064c'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bf53b5d85a12d80c0d399e26c8ad431d'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.ttr.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3f4abf6ecc24b87f92bb3a4b3215031d'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bbde39984238cf1bf18ec68299554106'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9f52a8d3cb1f77973c6216ef8eda69f2'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='fca22664af724664910576225a812439'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v1.tti.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(timestamp_ms%20-%20start_time_ms%20%2B%20duration_ms%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='95d2e950f95bc0011b61f2a1dec73238'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1552ece62bc68c32b27320cbeed0b4df'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e2b5c523bfcfc00a62eef2d6ea3f94ad'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='28307d72410c80d928f68eeba2366526'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0dea8074115055e6bada1b25f19e5f89'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='57f67d43d65b22b5ffc4be14ec9126a3'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='11c8b08685372f70319aed9bbb56ab12'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='efcabdd1565fcc5c0221ad16aeb1d686'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='d660dd0856a510dd53b4126ee6ffae4b'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='407be5aee265f4a91e286331496aa147'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a932400589ba2dadf58839d894c77fa2'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9ebadd98ff52a53c5fe5c628eb8fa29c'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.ttr.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttrDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6f7806d6612522c4fc9a09643050a3d7'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='49656525da1065c5e0c389f4a9ae531b'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='e5d8b53e2d47fdd6b5abe998c8e54d3d'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='61251b061f20752b315d13527835cd08'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='41efa9a9a85f81dfaa5255a47b5b7e9c'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='37a20b544a1dd889503985cc7675b66f'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='a40fc7f04879cc74d8896966f833579c'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1306f489aaad6d35c27d3acead962c0d'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='4287e229aba84947c23fa55bc66bbac2'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b0606d008b8784bc7475efffb4966f2a'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bfd949afabb81b26743918883fabd134'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ae5d448602917a5f79dc864168130de0'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='513c852098f4cd75d8e6815371648310'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='76025957f64dc0484dc83e67947fcaf5'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='3a7afd785e304ecd0f557e99f6fd1496'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='dba69a61ba05e8dde57e60622922caac'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti.shift.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiShift')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5ff79cce799ec7bc94a8da2d3ebc3fe3'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='6e47d874217868247f12283892c7e80a'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='52f7c9692fc0df0832c3b599c2025d7a'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='f9754400cbd108cd61e44b63ed140ce4'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.start.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawStart')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b9dd4f8db7e7083d8bf36fdb2a3aafd4'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='29caab2e2915b747539aa4517e6277bf'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='b1241189a7f182f408993e7e71a0407e'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='704ca800e7d6b75203201150460d3775'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.end.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawEnd')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='30f22299bb1ac480269733d34d76db98'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='5a11a5241ac51874c4d2f5f6c80716df'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    robotness,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        robotness,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='9d38b248245f1d60c86cb9ea2bc3f6fd'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    requester,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        requester,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ab71582a368dce6d85778a271850d08f'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
    service_white,
    regionName,
    page

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.firstScreen.metrics.v2.tti_raw.duration.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toInt32OrZero(info_values%5BindexOf(info_keys%2C%20'ttiRawDuration')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20portion%20%3D%20'firstScreen')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0,
        service_white,
        regionName,
        page
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ed6b05aea3e4abeced4cf3c4fb25d56a'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
    service_white,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
        service_white,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='c8a23b69f8274e12b32f2c61e24d7992'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
    service_white,
    robotness,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
        service_white,
        robotness,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='8eb9744ffe4f0afd5766512cacac46e0'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
    service_white,
    requester,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
        service_white,
        requester,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='0b55059fec54baf894d2763f972d1649'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
    service_white,
    regionName,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.stuffing.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'stuffing')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
        service_white,
        regionName,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        regionToName(regionToCountry(region), 'en') as regionName,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='1fbe08f15b8f272cdb0e484b2cf013bd'></a>market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
    service_white,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.total.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
        service_white,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='613f5dedaf574ed323ced7599d0600c5'></a>market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20robotness%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
    service_white,
    robotness,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.robotness.splits.%24%7Brobotness%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20robotness%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(extract(nanny_service_id%2C%20'robots')%20!%3D%20''%2C%20'robots'%2C%20'humans')%20as%20robotness%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
        service_white,
        robotness,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='ef9635923716e13969d19410c161a512'></a>market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20requester%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
    service_white,
    requester,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.requester.splits.%24%7Brequester%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20requester%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20if(info_values%5BindexOf(info_keys%2C%20'yandexLogin')%5D%20%3D%20''%2C%20'anonymous'%2C%20'logged-in')%20as%20requester%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
        service_white,
        requester,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
        if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester,
        arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
        replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget
)

GROUP BY metric_ts
ORDER BY cnt DESC
LIMIT 1
```
#### <a id='bd14c8562b026e38c9e41ae00537297d'></a>market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles

[Preview query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%0A%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20service_white%2C%0A%20%20%20%20regionName%2C%0A%20%20%20%20page%2C%0A%20%20%20%20widget%0A%0AFROM%20market.market_client_timers%0A%0AWHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%0AGROUP%20BY%20metric_ts%2C%0A%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A%0AORDER%20BY%20metric_ts%20LIMIT%2010)
```SQL
SELECT
    multiply(intDiv(timestamp, 60), 60) AS metric_ts,
    quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
    service_white,
    regionName,
    page,
    widget

FROM market.market_client_timers

WHERE date = today() and timestamp > now() - 60 * 60
    AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')

GROUP BY metric_ts,
    multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
    regionToName(regionToCountry(region), 'en') as regionName,
    arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page,
    replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget

ORDER BY metric_ts LIMIT 10
```

[Diagnostic query:](https://yql.yandex-team.ru/?query_type=CLICKHOUSE&query=use%20marketclickhouse%3B%0A%0ASELECT%20%0A%20%20%20%20'market-front-unified.market_client_timers.v2.%24%7Bservice_white%7D.regionName.splits.%24%7BregionName%7D.%24%7Bpage%7D.widgets.%24%7Bwidget%7D.metrics.hydrating.quantiles'%20AS%20title%2C%20%0A%20%20%20%20count()%20AS%20cnt%0A%20%20%20%20%20%0AFROM%20(%0A%20%20%20%20SELECT%0A%20%20%20%20%20%20%20%20multiply(intDiv(timestamp%2C%2060)%2C%2060)%20AS%20metric_ts%2C%0A%20%20%20%20%20%20%20%20quantilesTimingIf(0.5%2C0.6%2C0.7%2C0.80%2C0.90%2C0.95%2C0.97%2C0.99%2C0.995%2C0.997%2C0.999%2C1)(toUInt32OrZero(info_values%5BindexOf(info_keys%2C%20'hydrating')%5D)%2Cplatform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%20as%20value_0%2C%0A%20%20%20%20%20%20%20%20service_white%2C%0A%20%20%20%20%20%20%20%20regionName%2C%0A%20%20%20%20%20%20%20%20page%2C%0A%20%20%20%20%20%20%20%20widget%0A%20%20%20%20%0A%20%20%20%20FROM%20market.market_client_timers%0A%20%20%20%20%0A%20%20%20%20WHERE%20date%20%3D%20today()%20and%20timestamp%20%3E%20now()%20-%2060%20*%2060%0A%20%20%20%20%20%20%20%20AND%20(platform%20%3D%20'web'%20and%20regionToCountry(region)%20in%20(225%2C%20149%2C%20159%2C%20187)%20and%20service_white%20!%3D%20'undefined_service'%20and%20name%20%3D%20'widget')%0A%20%20%20%20%0A%20%20%20%20GROUP%20BY%20metric_ts%2C%0A%20%20%20%20%20%20%20%20multiIf(%20vhost%20in%20('market.yandex.ru'%2C'market.yandex.ua'%2C'market.yandex.by'%2C'market.yandex.kz')%2C%20'white_desktop'%2Cvhost%20in%20('m.market.yandex.ru'%2C'm.market.yandex.ua'%2C'm.market.yandex.by'%2C'm.market.yandex.kz')%2C%20'white_touch'%20%2C%20'undefined_service'%20)%20as%20service_white%2C%0A%20%20%20%20%20%20%20%20regionToName(regionToCountry(region)%2C%20'en')%20as%20regionName%2C%0A%20%20%20%20%20%20%20%20arrayJoin(%5B'any-page'%2C%20replaceAll(page_id%2C%20'%3A'%2C%20'_')%5D)%20as%20page%2C%0A%20%20%20%20%20%20%20%20replaceRegexpAll(info_values%5BindexOf(info_keys%2C%20'widgetName')%5D%2C'%5B%5Ea-zA-Z0-9%5D'%2C%20'')%20as%20widget%0A)%0A%0AGROUP%20BY%20metric_ts%0AORDER%20BY%20cnt%20DESC%0ALIMIT%201)
```SQL
SELECT 
    'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, 
    count() AS cnt
     
FROM (
    SELECT
        multiply(intDiv(timestamp, 60), 60) AS metric_ts,
        quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0,
        service_white,
        regionName,
        page,
        widget
    
    FROM market.market_client_timers
    
    WHERE date = today() and timestamp > now() - 60 * 60
        AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget')
    
    GROUP BY metric_ts,
        multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white,
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
    SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #2

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #3

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.buckets.${buckets_ttr}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_ttr FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms))) as buckets_ttr ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.buckets.${buckets_tti}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_tti FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(timestamp_ms - start_time_ms + duration_ms) > 32000, 'more_32000', toString(roundToExp2(timestamp_ms - start_time_ms + duration_ms))) as buckets_tti ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.buckets.${buckets_ttrStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_ttrStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')])))) as buckets_ttrStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.buckets.${buckets_ttrEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_ttrEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')])))) as buckets_ttrEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.buckets.${buckets_ttrDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_ttrDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')])))) as buckets_ttrDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.buckets.${buckets_ttiStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_ttiStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')])))) as buckets_ttiStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.buckets.${buckets_ttiEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_ttiEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')])))) as buckets_ttiEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.buckets.${buckets_ttiDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_ttiDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')])))) as buckets_ttiDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.buckets.${buckets_ttiShift}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_ttiShift FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')])))) as buckets_ttiShift ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.buckets.${buckets_ttiRawStart}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_ttiRawStart FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')])))) as buckets_ttiRawStart ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.buckets.${buckets_ttiRawEnd}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_ttiRawEnd FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')])))) as buckets_ttiRawEnd ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.buckets.${buckets_ttiRawDuration}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, buckets_ttiRawDuration FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, if(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])) > 32000, 'more_32000', toString(roundToExp2(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')])))) as buckets_ttiRawDuration ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, robotness, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #4

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, requester, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hps' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.buckets.${buckets_stuffing}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, widget, buckets_stuffing FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')])))) as buckets_stuffing ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.buckets.${buckets_hydrating}' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, count() / 60 as value_0, service_white, regionName, page, widget, buckets_hydrating FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget, if(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])) > 32000, 'more_32000', toString(roundToExp2(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')])))) as buckets_hydrating ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.ttr.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v1.tti.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(timestamp_ms - start_time_ms + duration_ms,platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #5

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.ttr.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttrDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti.shift.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiShift')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```
### Portion #6

```SQL
SELECT * FROM (
    SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.start.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawStart')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.end.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawEnd')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, robotness, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, requester, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.firstScreen.metrics.v2.tti_raw.duration.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toInt32OrZero(info_values[indexOf(info_keys, 'ttiRawDuration')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') as value_0, service_white, regionName, page FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and portion = 'firstScreen') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0, service_white, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0, service_white, robotness, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0, service_white, requester, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.stuffing.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'stuffing')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0, service_white, regionName, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.total.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0, service_white, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.robotness.splits.${robotness}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0, service_white, robotness, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(extract(nanny_service_id, 'robots') != '', 'robots', 'humans') as robotness, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.requester.splits.${requester}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0, service_white, requester, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, if(info_values[indexOf(info_keys, 'yandexLogin')] = '', 'anonymous', 'logged-in') as requester, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
    UNION ALL SELECT 'market-front-unified.market_client_timers.v2.${service_white}.regionName.splits.${regionName}.${page}.widgets.${widget}.metrics.hydrating.quantiles' AS title, count() AS cnt FROM ( SELECT multiply(intDiv(timestamp, 60), 60) AS metric_ts, quantilesTimingIf(0.5,0.6,0.7,0.80,0.90,0.95,0.97,0.99,0.995,0.997,0.999,1)(toUInt32OrZero(info_values[indexOf(info_keys, 'hydrating')]),platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') as value_0, service_white, regionName, page, widget FROM market.market_client_timers WHERE date = today() and timestamp > now() - 60 * 60 AND (platform = 'web' and regionToCountry(region) in (225, 149, 159, 187) and service_white != 'undefined_service' and name = 'widget') GROUP BY metric_ts, multiIf( vhost in ('market.yandex.ru','market.yandex.ua','market.yandex.by','market.yandex.kz'), 'white_desktop',vhost in ('m.market.yandex.ru','m.market.yandex.ua','m.market.yandex.by','m.market.yandex.kz'), 'white_touch' , 'undefined_service' ) as service_white, regionToName(regionToCountry(region), 'en') as regionName, arrayJoin(['any-page', replaceAll(page_id, ':', '_')]) as page, replaceRegexpAll(info_values[indexOf(info_keys, 'widgetName')],'[^a-zA-Z0-9]', '') as widget ) GROUP BY metric_ts ORDER BY cnt DESC LIMIT 1
) ORDER BY cnt DESC
```

