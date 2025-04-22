## Импорт библиотеки
Перед использованием необходимо проимпортировать библиотеку сдедующим образом:

```(yql)
PRAGMA File('soffers_udf.so', 'https://proxy.sandbox.yandex-team.ru/last/MARKET_SOFFERS_UDF?attrs={"released":"stable"}');
PRAGMA udf('soffers_udf.so');
```

## Парсинг профилей из таблиц State:
```(yql)
use senecavla;

PRAGMA File('soffers_udf.so', 'https://proxy.sandbox.yandex-team.ru/last/MARKET_SOFFERS_UDF?attrs={"released":"stable"}');
PRAGMA udf('soffers_udf.so');

SELECT SOffers::ParseContentOfferProfile(TableRow()) from `//home/market/testing/backbone/offers_store/state/ContentOffers`;
```

## Парсинг профилей из сериализованного протобуфа:
```(yql)
SELECT SOffers::ParseContentOfferProfileProto(ContengOfferProfileDump)
```

## Релизный пайплайн в CI
 - [CI](https://a.yandex-team.ru/projects/backbone/ci/releases/timeline?dir=market%2Fbackbone%2Foffers_store%2Fudf&id=release-udf)
