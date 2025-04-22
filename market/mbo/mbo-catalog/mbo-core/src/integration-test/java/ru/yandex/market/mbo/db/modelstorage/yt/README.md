Тесты YtRangeIdGeneratorTest и  YtModelStorageTest зависят от доступности YT.

Если прилег хан или учения в сасово, можно сделать две вещи:
1) mbo.yt.cluster=arnold в common-yt-test.properties
2) Подхачить проперти, которые тянутся из etcd (к сожалению, все три инстанса тестинговых в сасово)
Можно просто скачать файлы, datasources.propertires и mbo-search.properties с аиды.
Вот тут лежат:/etc/yandex/market-datasources/
Тут еще может понадобится и tnsnames.ora подхачить, что опять же можно с аиды взять.

И снова тестироваться локально, ура! :)

