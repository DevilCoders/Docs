## Как канонизировать тест
1. `./ya make ads/bsyeti/caesar/libs/ml/ut -rtA -F TBannerTsarComputerTest::Canon --test-param canonize-to=/absolute/path/to/any/directory/banner_tsar_sample.yson`
2. `ya upload --ttl=inf ./banner_tsar_sample.yson`
3. Поменять resource id в `ya.make`'е
