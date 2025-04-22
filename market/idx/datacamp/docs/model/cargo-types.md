# Карготипы

Карготип (cargo type) - тип груза.
Разметка карготипами msku и офферов необходима для процессов доставки и хранения товаров (не везти в постамат крупногабарит, не хранить пахучее рядом с впитывающим запахи).
Ознакомиться со списком карготипов можно тут:
- [документация](https://yandex.ru/dev/market/delivery-service/doc/dg/concepts/types.html#types__Item)
- [YQL запрос, есть id параметров](https://yql.yandex-team.ru/Operations/YZNxSZfFt8L5-UjR4EYcq_QC9pJJAyveWY0vvjYlLNg=)

## Быстрые карготипы
### Описание пайплайна
Пайплайн построен на основе пайплайна [быстрой доставки msku](https://wiki.yandex-team.ru/market/development/indexer/arxitektura-marketnogo-indeksatora/offer-repository/bystraja-dostavka-dannyx-na-sklad-iz-mdm-i-mbo/?from=%2Fusers%2Fcaramelo%2Fbystraja-dostavka-dannyx-na-sklad-iz-mdm-i-mbo).

- После внесения изменений в описание msku со стороны mdm & mbo отправляется сообщение в топик [market-mbo/prod/datacamp/datacamp-render-model](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_writeSession&graph=auto&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=MessagesWritten%2A&Topic=%21total&Producer=%21total&l.Account=market-mbo&l.TopicPath=market-mbo%2Fprod%2Fdatacamp%2Fdatacamp-render-model&b=1d&e=). График чтения: [тут](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_readSession&graph=auto&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&Topic=%21total&Producer=%21total&l.Account=market-mbo&l.sensor=MessagesRead&checks=%2Bmarket-indexer%40prod%40white%40datacamp-consumer-original%2C%20market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%2C%20Iva%2C%20Iva%3Bmarket-indexer%40prod%40white%40datacamp-consumer-original%2C%20market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%2C%20Man%2C%20Man%3Bmarket-indexer%40prod%40white%40datacamp-consumer-original%2C%20market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%2C%20Myt%2C%20Myt%3Bmarket-indexer%40prod%40white%40datacamp-consumer-original%2C%20market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%2C%20Sas%2C%20Sas%3Bmarket-indexer%40prod%40white%40datacamp-consumer-original%2C%20market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%2C%20Vla%2C%20Vla&l.TopicPath=market-mbo%2Fprod%2Fdatacamp%2Fdatacamp-render-model&b=1d&e=)
- Полученная msku мержится в таблицу [datacamp/msku/msku](https://yt.yandex-team.ru/arnold/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/msku/msku).
- Если на msku изменился один из карготипных параметров, и изменение значимо, то msku отправляется в msku_miner через топик [iris-msku-controllers-to-miner](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_writeSession&graph=auto&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=MessagesWritten%2A&Topic=%21total&Producer=%21total&l.Account=market-indexer&l.TopicPath=market-indexer%2Fprod%2Funited%2Firis-msku-controllers-to-miner&b=1d&e=) с флагом [CARGO_TYPE_TO_DATACAMP](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/lib/proto_helpers/datacamp_msku.h?rev=r8588720#L11) в поле [msku_route_flags](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/models/MarketSku.proto#L49). Флаги в поле используются для разведения потоков обновления msku, направленных к офферам и к iris/складам.
  Нюансы:
  - Карготипные параметры отличаются от других именем - xsl_name такого параметра всегда начинается на "cargoType".
  - Только "назначенный" на msku карготип должен оказаться на оффере. Карготип считается "назначенным" на msku при совпадении двух условий: карготип есть в списке параметров msku, в поле bool_value этого параметра указано true. Следовательно, например: 
    - если на msku не было карготипа Х, а затем он появился с bool_value=false - это изменение не значимо в контексте пайплайна быстрых карготипов.
    - а изменение bool_value=true на bool_value=false будет обработано.
- В [msku_miner](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/msku_miner) мы получаем список офферов, замапленных на msku(1) и убеждаемся, что обновленная msku совпадает с approved msku на оффере(2) (офферы, для которых это не так игнорируем). Далее формируется набор мини-офферов (идентификаторы + карготипы), которые отправляются в пайпер через топик [datacamp-offers-from-msku-miner](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_writeSession&graph=auto&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=MessagesWritten%2A&Topic=%21total&Producer=%21total&l.Account=market-indexer&l.TopicPath=market-indexer%2Fprod%2Funited%2Fdatacamp-offers-from-msku-miner&b=1d&e=).
  Подробней:
  - (1): используется табличка [mboc_offers](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/mboc_offers/states) - это копия таблицы [mboc_offers_expanded_sku/actual-state](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/mbo/stat/mboc_offers_expanded_sku/actual-state), которую мы обновляем у себя раз в 30 минут.
  - (2): посредством запроса в таблицу basic_offers
- В [miner](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/miner) также перешли на использование быстрее обновляемой таблицы [datacamp/msku/msku](https://yt.yandex-team.ru/arnold/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/msku/msku). Обогащение карготипами из этой таблицы реализовано в [datacamp_msku_enricher](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/miner/processors/datacamp_msku_enricher), работает при ENABLE_FAST_CARGO_TYPES_PIPELINE=true.

<iframe height="400" width="100%" src="https://jing.yandex-team.ru/files/thesonsa/offer_cargo_type_.png" frameborder="0"></iframe>

### Особые случаи
- Изменение мскю: информация об изменении msku приходит через топик [datacamp/offer-state-updates](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqtabletAggregatedCounters&l.host=*&l.TopicPath=market-mbo%2Fprod%2Fdatacamp%2Foffer-state-updates&l.OriginDC=*&l.ConsumerPath=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&l.sensor=MessageLagByCommitted&graph=auto&b=1d&e=). На поля маппинга подписан майнер, при перемайнинге набор карготипов становится консистентен с новым маппингом. 
  Благодаря проверкам маппинга через базовую таблицу даже при устаревшем маппинге в таблице mboc_offers не возникает проблемы - для оффера игнорируются обновления старой msku. Обновления его новой msku начнут учитываться после того, как в mboc_offers будет отображен новый маппинг.
  То есть после получения нового маппинга возможно непрорастание обновлений карготипов новой msku на оффер до появления следующей таблицы mboc_offers. Недостаток данных исправляется при регулярном перемайнинге.
- Особенность с карготипами ДБС
  ДБС офферы не обрабатываются МДМ.
  Поэтому для них реализована отдельная разметка крупногабаритными карготипами в зависимости от категории товара и его размеров.
  Подробней можно почитать в [проектном тикете](https://st.yandex-team.ru/MARKETINDEXER-39711).
  Карготипы синих перевозятся в базовую часть, дбс-ные карготипы остаются в сервисной.
  При формировании оффера в выгрузки для поколений эта особенность учитывается, карготипы [берутся](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/lib/conversion/OfferConversions.cpp?rev=r8714319#L1280) из разных мест.
- ..дописать про хрусталь))

### Полезные ссылки
- графики по flow msku в хранилище
  - [прод](https://yasm.yandex-team.ru/template/panel/MskuDataflowProduction)
  - [тестинг](https://yasm.yandex-team.ru/template/panel/MskuDataflowTesting)
- msku в интерфейсе mdm - тут отображены не все карготипы (например, нет пачкающих), но в части ситуаций позволяет сориентироваться. В тестинге можно использовать для тестирования (права запрашивала у [Алексея Сахарова](https://staff.yandex-team.ru/cloudcat)).
  - [прод](https://mdm.market.yandex-team.ru/mdm/msku/100852850756)
  - [тестинг](https://mdm-testing.market.yandex-team.ru/mdm/msku/100648300244) 
- msku в интерфейсе mbo - можно посмотреть историю изменений за период по разным параметрам, в том числе посмотреть, менялся ли значимо какой-то карготип
  - [прод](https://mbo.market.yandex-team.ru/ui/audit?entityId=100852850756&finishDate=2021-10-07T14%3A49%3A18.836Z&hasFilters=1&hideSystemProperties=0&page=1&perPage=350&requestType=GROUP_BY_EVENT_ENTITY_USER&startDate=2021-09-27T14%3A49%3A18.000Z)
  - [тестинг](https://mbo-testing.market.yandex-team.ru/ui/audit?entityId=100648300244&finishDate=2021-10-07T14%3A49%3A18.836Z&hasFilters=1&hideSystemProperties=0&page=1&perPage=350&requestType=GROUP_BY_EVENT_ENTITY_USER&startDate=2021-09-27T14%3A49%3A18.000Z)
- [запрос](https://yql.yandex-team.ru/Operations/YV7Ut5fFtyYfx4UcLg_H3KetTaeXNrl1JAB_XcJJu38=) про назначенные/активные карготипы msku
- проектный тикет [MARKETINDEXER-40282](https://st.yandex-team.ru/MARKETINDEXER-40282)

### Как выключить
- msku_miner:
  - Если что-то будет не так с запросами в базовую таблицу, выключать так:
  `MSKU_MINER_ENABLE_MSKU_TO_OFFER_CONVERTER=false` - приведет к [выходу вот тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/msku_miner/lib/msku_to_offer_converter/msku_to_offer_converter.cpp?rev=r8706770#L65-67).
  - Если с запросами ок, но не хотим писать в таблицы обновления, выключать так:
  `MSKU_MINER_ENABLE_MSKU_TO_OFFER_CONVERTER_DRYRUN=true` - [выход тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/msku_miner/lib/msku_to_offer_converter/msku_to_offer_converter.cpp?rev=r8706770#L168-171)
- miner:
  `ENABLE_FAST_CARGO_TYPES_PIPELINE=false`:
  - [выключит](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/miner/processors/datacamp_msku_enricher/datacamp_msku_enricher.cpp?rev=r8710492#L139) использование быстрой таблицы
  - [включит](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/miner/processors/cargo_types_enricher/processor.cpp#L49) использование медленной
