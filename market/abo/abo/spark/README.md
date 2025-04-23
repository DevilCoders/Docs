# Генерация java-классов для спарка 
[Старая документация](https://a.yandex-team.ru/arc/trunk/arcadia/market/abo/abo/spark-models-generated/spark.md?rev=5000578)

В основных .xsd есть корневой элемент `Response`, из-за этого, если передать генератору > 1 файла, он сыпется от того, что одинаковый элемент встречается дважды, поэтому мы их обрабатываем по одному.  
Также могут быть конфликты, когда есть две сущности с одинаковым именем в `CommonTypes.xsd` и отдельно. На данный момент это `RetailSalesSummary` 
([раз](https://a.yandex-team.ru/arc/trunk/arcadia/market/abo/abo/spark/xsd/CommonTypes.xsd?rev=7410525#L2851),
[два](https://a.yandex-team.ru/arc/trunk/arcadia/market/abo/abo/spark/xsd/RetailSalesSummary.xsd?rev=7410525#L2)).
В этом случае нужно явно задать другое имя в [ya.make](https://a.yandex-team.ru/arc/trunk/arcadia/market/abo/abo/spark/ya.make?rev=6862787#L17).
