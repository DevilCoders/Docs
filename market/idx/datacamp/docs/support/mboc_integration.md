## Траблшутинг интеграции ЕОХ <-> MBOC

В документе описан алгоритм, которому нужно следовать, во время расследования проблем по части обработки контента между Хранилищем и MBOC.

### Как оформить тикет в очередь Хранилища
Если нужно поставить тикет в очередь Хранилища, то стоит сделать следующее:
- выбрать [очередь MARKETINDEXER](https://st.yandex-team.ru/createTicket?queue=MARKETINDEXER)
- проставить ему теги: datacamp_support, datacamp_mboc_integration и модель продажи (DBS, FBY, FBS и т.д.).
- для корректной развесовки нужно еще заполнить shop_id в поле MBI -> ID партнеров (для продовых партнеров)
- указать среду тестинг / прод
- добавьте в тикет все результаты вашего расследования по пунктам
- для того чтобы исполнитель тикета увидел ту же ситуацию, что и вы, сохраните в тикет не только http-запросы, которым пользовались, но и ответы полученные от них

### Что такое консистентность с точки зрения MBOC?
Консистентный с т.з. MBOC оффер - это такой, для которого со свежими партнерскими данными хоть раз сходили в UltraController.
Техническим языком:
1) [версия контента, от которого зависит ответ UC](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r7724646#L217) == [версии данных, с которыми действительно ходили в UC](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r7724646#L180)
2) Как смотреть, пример
   ```
   curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10462389/offers/TestAV53/basic?format=json" | python -m json.tool
   ...
   "content": {
       "market" : {
           "real_uc_version": {
               "counter": 48      <--- версия данных с которыми ходили в UC
           },
       ...
       "status": {
           "consistency": {
               "mboc_consistency": true <---  оффер консистентный
           },
           "version": {
               ...
               "uc_data_version": {
                   "counter": 48   <--- версия данных для похода в uc
               }
           }
           ...
   },
   ```

### Алгоритм расследования потерянных данных между ЕОХ <-> MBOC
1) Убедиться, что оффер консистентный
    - запрашиваем базовую часть оффера, находим поле консистентности
    - тестинг ```http://datacamp.white.tst.vs.market.yandex.net/v1/partners/{your_business_id}/offers/basic?offer_id={your_shop_sku}&format=json```
    - прод ```http://datacamp.white.vs.market.yandex.net/v1/partners/{your_business_id}/offers/basic?offer_id={your_shop_sku}&format=json```
    - как по офферу определять консистентность см. выше
    - пример
    ```
    curl "http://datacamp.white.vs.market.yandex.net/v1/partners/920123/offers/basic?offer_id=10639&format=json" | python -m json.tool | grep "mboc_consistency"
    "mboc_consistency": true,
    ```
2) Если оффер не консистентный, проверяем
    - если оффер был обновлен недавно (до 1 часа), то ждем ориентируясь на очереди майнера
    - есть ли проблема с майнером с входными очередями майнера ([прод](https://grafana.yandex-team.ru/d/83-6mZm7k/vteam-tech-metrics?viewPanel=66&orgId=1&from=now-2d&to=now&refresh=1m), [тестинг](https://solomon.yandex-team.ru/?b=2021-07-15T17%3A26%3A14.481Z&e=2021-07-16T17%3A26%3A14.481Z&project=kikimr&cluster=lbk&service=pqtabletAggregatedCounters&graph=auto&Account=market-indexer&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=ReadTimeLagMs&ConsumerPath=market-indexer%2Ftesting%2Fwhite%2Fdatacamp-consumer-original&TopicPath=market-indexer%2Ftesting%2Funited%2Fdatacamp-offers-to-miner&partition=-&user_counters=PersQueue&stack=false))
    - есть ли проблема чтением данных из выходной очереди майнера ([прод](https://grafana.yandex-team.ru/d/83-6mZm7k/vteam-tech-metrics?viewPanel=64&orgId=1&from=now-2d&to=now&refresh=1m), [тестинг](https://solomon.yandex-team.ru/?b=2021-07-15T17%3A21%3A03.448Z&e=2021-07-16T17%3A21%3A03.448Z&project=kikimr&cluster=lbk&service=pqtabletAggregatedCounters&graph=auto&Account=market-indexer&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=ReadTimeLagMs&ConsumerPath=market-indexer%2Ftesting%2Fwhite%2Fdatacamp-consumer-original&TopicPath=market-indexer%2Ftesting%2Funited%2Fdatacamp-offers-from-miner&partition=-&user_counters=PersQueue&stack=false))
    - если проблема есть, то ей занимается дежурный Хранилища (см. [процедуру дежурств](https://docs.yandex-team.ru/market-datacamp/support/processes#dezhurstva)). Эффект: после изменений оффер становится консистентным очень долго.
3) Если п. 3 не подходит и оффер не становится консистентным, то нужно поставить тикет в саппорт хранилища (см. выше как это сделать)
4) Если оффер консистентный, проверяем, что он попал в очередь логброкера
    - [yql скрипт](https://yql.yandex-team.ru/Operations/X_8ad9K3DAcdS5Q38hR-o2spKguGC1NFz7GsbuOqPk8=) (данные появляются через ~1.5-2 часа)
    - когда найдете оффер стоит обратить на [версию актуальных данных](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r7724646#L217) у него 
    - пример для [запроса](https://yql.yandex-team.ru/Operations/X_8ad9K3DAcdS5Q38hR-o2spKguGC1NFz7GsbuOqPk8=)
      ```
      iso_time = "2021-01-13 17:04:47" <--- когда в топик попало
      united_offers = { <--- оффера, внимание! это батч офферов - сначала найдите внутри свой, потом смотрите на нем версию контента
      ...
      "status" = {
         ...
         "consistency" = {
           "mboc_consistency" = %true
         };
        "version" = {
          "actual_content_version" = {
            "counter" = 8027    <--- версия контента, которая уехала в MBOC
          }
        }
      }
      ```
    - если консистентный оффер не лег в топики, то нужно поставить тикет в саппорт хранилища (см. выше как это сделать)
5) Используйте диагностическую ручка в КИ, которая дает детальную информацию по тому как обрабатывался оффер в КИ
    - тестинг ```https://cm-testing.market.yandex-team.ru/api/dev/datacamp/offer-info/business/{business_id}/offer/{shop_sku}```
    - прод ```https://cm.market.yandex-team.ru/api/dev/datacamp/offer-info/business/{business_id}/offer/{shop_sku}```
    - пример 
   ```
   https://cm.market.yandex-team.ru/api/dev/datacamp/offer-info/business/920123/offer/10639
    <DatacampOfferInfo>
        <businessId>920123</businessId>
        <offerId>10639</offerId>
        <groupId/>
        <dcOfferStatus>NOT_UP_TO_DATE</dcOfferStatus>
        <mbocOfferStatus>UP_TO_DATE</mbocOfferStatus>
        <contentProcessingOfferStatus>NOT_UP_TO_DATE</contentProcessingOfferStatus>
        <shouldBeProcessed>false</shouldBeProcessed>
        <shouldBeStored>false</shouldBeStored>
        <shouldProcessContent>true</shouldProcessContent>
        <datacampLink>http://datacamp.white.vs.market.yandex.net/v1/partners/920123/offers/10639/basic?format=json</datacampLink>
        <datacampGroupLink/>
        <auditLink>https://mbo.market.yandex.ru/ui/audit?entityTypeList=CM_BLUE_OFFER&entityId=23254812</auditLink>
        <offerLink>http://cm-api.vs.market.yandex.net/proto/mboMappingsService/searchMappingsByBusinessKeys?q={keys:[{"business_id":920123,"offer_id":"10639"}]}</offerLink>
        <agLink>http://autogen-api.vs.market.yandex.net:34540/partner-content/api/develop/dcp/response/920123?offerId=10639&tvm=false</agLink>
        <messages>
            <messages>Offer content system response version is missing in datacamp</messages>
            <messages>Picture avatars.mds.yandex.net/get-mpic/1603927/img_id4245611703192275778.jpeg/orig is not downloaded yet</messages>
            <messages>Has supplier 555360 in migration, should save</messages>
            <messages>Offer has no service offers to process</messages>
            <messages>Datacamp not received response for offer version, stored in MBOC</messages>
            <messages>Offer is ready to create content, but not in queue and is not processed</messages>
        </messages>
    </DatacampOfferInfo>
   ```
6) Проверяем, был ли ответ MBOC
    - [yql скрипт](https://yql.yandex-team.ru/Operations/YHSCWL94hnvrCBoOODuOCviTGqwGkLlZWbFYomk61ZU=) (данные появляются через ~1.5-2 часа)
    - смотрим [на версию данных](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/ContentStatus.proto?rev=r7747645#L52), по которым MBOC давал ответ. 
      Если они все меньше, чем искомая версия из п. 5, то нужно обратиться [за помощью в MBO](https://nda.ya.ru/3TYVVV) (пожалуйста, приложите все расследование)
    - пример для [запроса](https://yql.yandex-team.ru/Operations/X_8lX1PzVIU9WlawedcHpPu08kAtM4ePiFh7zgvpa8E=)
      ```
      iso_time = ""2021-01-13 17:38:00"" <--- когда в топик попало
      united_offers = { <--- оффера, внимание! это батч офферов - сначала найдите внутри свой, потом смотрите на нем версию
          ...
          "content" = {
              ...
              "status" = {
              ...
              "status_content_version" = {
                "counter" = 6918       <--- версия данных по которым тут едет ответ от MBOC
              }
          }
      }
      ```
8) Если ответ от MBOC был, то проверяем его запись в ЕОХ
    - запрашиваем базовую часть оффера, находим [версию, которые получили от MBOC](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/ContentStatus.proto?rev=r7747645#L52)
    - тестинг ```http://datacamp.white.tst.vs.market.yandex.net/v1/partners/{your_business_id}/offers/basic?offer_id={your_shop_sku}&format=json```
    - прод ```http://datacamp.white.vs.market.yandex.net/v1/partners/{your_business_id}/offers/basic?offer_id={your_shop_sku}&format=json```
     - пример
      ``` 
      curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10462389/offers/basic?offer_id=TestAV53&format=json" | python -m json.tool
      {
          "offers": [
          {
              "content": {
              ...
              "status": {
                  ...
                  "status_content_version": {
                    "counter": 368  <--- версия, которую получили от MBOC (проблема только когда версия меньше ожидаемой)
                  }
              }
          ...
      }
    ```
    - смотрим есть ли проблема чтением топика пайпера с данными из мбока ([прод](https://grafana.yandex-team.ru/d/83-6mZm7k/vteam-tech-metrics?viewPanel=62&orgId=1&from=now-2d&to=now&refresh=1m), [тестинг](https://solomon.yandex-team.ru/?b=2021-07-15T17%3A22%3A41.217Z&e=2021-07-16T17%3A22%3A41.217Z&project=kikimr&cluster=lbk&service=pqtabletAggregatedCounters&graph=auto&Account=market-mbo&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=ReadTimeLagMs&ConsumerPath=market-indexer%2Ftesting%2Fwhite%2Fdatacamp-consumer-original&TopicPath=market-mbo%2Ftest%2Fdatacamp%2Foffer-state-updates&partition=-&user_counters=PersQueue&stack=false))
    - если проблема есть, то ей занимается дежурный Хранилища (см. [процедуру дежурств](https://docs.yandex-team.ru/market-datacamp/support/processes#dezhurstva))
    - если проблемы нет, то нужно поставить тикет (см. выше как это сделать)
9) Все данные доехали
    - запрашиваем базовую часть оффера, находим [версию, которые получили от MBOC](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/ContentStatus.proto?rev=r7747645#L52 ) и [версию данных, которую отправляли](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r7747645#L217)
   - тестинг ```http://datacamp.white.tst.vs.market.yandex.net/v1/partners/{your_business_id}/offers/basic?offer_id={your_shop_sku}&format=json```
   - прод ```http://datacamp.white.vs.market.yandex.net/v1/partners/{your_business_id}/offers/basic?offer_id={your_shop_sku}&format=json```
   - пример
      ``` 
      curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10462389/offers/basic?offer_id=TestAV53&format=json" | python -m json.tool
      {
      "offers": [
      {
          "content": {
          ...
              "status": {
                  ...
                  "status_content_version": {
                    "counter": 368  <--- версия, которую получили от MBOC
                  }
              }
          }
          ...
          "status": {
              "version": {
                  "actual_content_version": {
                    "counter": 368   <--- версия, которую отправляли в MBOC
                  },
              }
      ...
      ```