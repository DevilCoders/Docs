# Добавление полей в оффер
Предположим, стоит задача добавить в оффер minRentPeriod - минимальный период аренды (в месяцах).

## Куда добавлять
1. XML-схема фида. Она проверяется в feedloader. Названия полей в XML-фиде (и схеме) должны быть в kebab-case: смотрим min-rent-period
   * [realty.xsd](https://a.yandex-team.ru/arcadia/classifieds/realty/feedloader/partnerdata-feedloader/src/main/resources/xsd/realty.xsd)
   * [realty-format.xsd](https://a.yandex-team.ru/arcadia/classifieds/realty/scripts/commercial-realty/feedformat/realty-format.xsd)

    В самом фиде (когда будем тестировать) добавлять нужно так:
    ```
    <offer ...>
    ...
    <min-rent-period>7</min-rent-period>
    </offer>
    ```

    Бывают более сложные типы данных - например, price с указанием валюты (ищем примеры по словам "price" или "currency").


2. Эти классы непосредственно влияют на парсинг из XML. Здесь поля именуются в camelCase: minRentPeriod
   * [RawOffer.java](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-model/src/main/java/ru/yandex/realty/model/raw/RawOffer.java)
   * [RawOfferImpl.java](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-model/src/main/java/ru/yandex/realty/model/raw/RawOfferImpl.java)

    И также нужно добавить методы getMinRentPeriod, setMinRentPeriod. Парсинг из XML делается через reflection, всё определяется именами и наличием getter/setter.


3. Добавить поле в schema-registry (protobuf):
   * [offer.proto](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/realty/offer/vos/offer.proto)

    Здесь поле называется minimal_period и находится в контексте объекта RentOffer (который находится в VosOfferSource), т.к. оно имеет смысл только в контексте аренды (но не продажи).


4. Добавить конвертацию RawOffer <-> VosOfferSource:
   * [VosOfferSourceFromMessage.scala](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-common/src/main/scala/ru/yandex/realty/converters/vos/VosOfferSourceFromMessage.scala)
   * [VosOfferSourceToMessage.scala](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-common/src/main/scala/ru/yandex/realty/converters/vos/VosOfferSourceToMessage.scala)

    Здесь встречаются оба названия - minimalPeriod и minRentPeriod. В идеале, конечно, именовать стоит более целостно. При более сложных типах данных придётся извернуться (смотрим по словам "price" или "currency").


5. добавить min_rent_period в модель RealtyOffer (protobuf):
   * [realty_offer_model.proto](https://a.yandex-team.ru/arcadia/classifieds/realty/vos2/vos2-model-proto/src/main/proto/realty/realty_offer_model.proto)


6. Добавить поле в ручки создания/редактирования оффера и черновика в vos:
   * [UpdateOfferInfo.scala](https://a.yandex-team.ru/arcadia/classifieds/realty/vos2/realty-vos-api/src/main/scala/ru/yandex/vos2/api/model/UpdateOfferInfo.scala)
   * [RealtyOfferCommonInformation.scala](https://a.yandex-team.ru/arcadia/classifieds/realty/vos2/realty-vos-api/src/main/scala/ru/yandex/vos2/api/model/RealtyOfferCommonInformation.scala)

   UpdateOfferInfo - это entity, которая приходит в ручки. В нашем случае minRentPeriod лучше добавлять в RealtyOfferCommonInformation (который вложен в UpdateOfferInfo). Сами ручки находятся в UserOffersHandler в vos.


7. Добавить код, который перекладывает minRentPeriod из RealtyOfferCommonInformation в RealtyOffer:
   * [RealtyOfferExtractor.scala](https://a.yandex-team.ru/arcadia/classifieds/realty/vos2/realty-vos-api/src/main/scala/ru/yandex/vos2/api/directives/utils/RealtyOfferExtractor.scala)


8. Добавить в конверторы Offer/RealtyOffer <-> StoredOffer/VosOfferSource, чтобы оффер сохранялся/доставалcя в MySQL в vos:
   * [ModelConverterOperativeToStored.scala](https://a.yandex-team.ru/arcadia/classifieds/realty/vos2/vos2-realty-core/src/main/scala/ru/yandex/vos2/realty/dao/offers/converter/ModelConverterOperativeToStored.scala)
   * [ModelConverterStoredToOperative.scala](https://a.yandex-team.ru/arcadia/classifieds/realty/vos2/vos2-realty-core/src/main/scala/ru/yandex/vos2/realty/dao/offers/converter/ModelConverterStoredToOperative.scala)

    Ищем minRentPeriod/minimalPeriod, в нашем случае это будет в контексте методов extractRentOffer и fillRentOfferFields. Ничего менять в DAO для MySQL не нужно, т.к. оффер сохраняется целиком в виде сериализованного protobuf.


9. Добавить поле в модель UnifiedOffer ("новая модель").
   * [unified_offer.proto](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/realty/offer/unified_offer.proto)
   * [offer_type_part.proto](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/realty/offer/unified_offer_parts/offer_type_part.proto) - в нашем случае поле min_period находится здесь во вложенном объекте RentOffer


10. Добавить в Offer ("старую модель") методы getMinRentPeriod, setMinRentPeriod, которые будут проксировать в "новую модель":
    * [Offer.java](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-model/src/main/java/ru/yandex/realty/model/offer/Offer.java)


11. Добавить поле min_rent_period в RawOfferMessage, OfferMessage (protobuf):
    * [RealtySchema.proto](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-model/src/main/proto/RealtySchema.proto)

    min_rent_period был ещё добавлен в TransactionMessage, но так больше делать не нужно (это издержки старой модели).


12. Добавить в конверторы Offer <-> OfferMessage, RawOffer <-> RawOfferMessage:
    * [OfferProtoConverter.java](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-model/src/main/java/ru/yandex/realty/model/serialization/OfferProtoConverter.java)
    * [RawOfferProtoConverter.java](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-model/src/main/java/ru/yandex/realty/model/serialization/RawOfferProtoConverter.java)

    Ищем по minRentPeriod


13. Добавить в подходящий unifier, чтобы заполнить поле в Offer/UnifiedOffer:
    * [CompleteUnifier.scala](https://a.yandex-team.ru/arcadia/classifieds/realty/realty3-indexer-common/src/main/scala/ru/yandex/realty/unifier/CompleteUnifier.scala)

    Находим здесь подходящий unifier (или добавляем новый). В данном случае есть RentParamsUnifier, в нём ищем minRentPeriod:
    * [RentParamsUnifier.scala](https://a.yandex-team.ru/arcadia/classifieds/realty/realty3-indexer-common/src/main/scala/ru/yandex/realty/unifier/RentParamsUnifier.scala)


14. Добавить minRentPeriod ещё сюда (требуется где-то в vos для выдачи оффера):
    * [FullOfferRenderer.scala](https://a.yandex-team.ru/arcadia/classifieds/realty/vos2/vos2-realty-core/src/main/scala/ru/yandex/vos2/realty/api/rendering/FullOfferRenderer.scala)


15. Чтобы выдать наше поле на карточке оффера (cardWithViews.json)
    * [OfferResponse.java](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-searcher/src/main/java/ru/yandex/realty/searcher/response/OfferResponse.java)
    * [OfferResponseBuilder.java](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-searcher/src/main/java/ru/yandex/realty/searcher/response/builders/OfferResponseBuilder.java)

    Ищем minRentPeriod


16. Чтобы выдать наше поле в ручках редактирования оффера (user/offers/`offerId`/edit) и карточки оффера (user/me/offers/`offerId`/card) для мобильных аппов:
    * [conditions_part.proto](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/realty/offer/unified_offer_parts/conditions_part.proto)
    * [OfferDataToFilterStateTransformer.scala](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-gateway/src/main/scala/ru/yandex/realty/transformers/OfferDataToFilterStateTransformer.scala)
    * [controls_index.json](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-gateway/src/main/resources/controls_index.json)
    * [controls_decl.json](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-gateway/src/main/resources/controls_decl.json)

    Смотрим minRentPeriod и minimal_period. Json-файлы здесь - это "форма создания оффера".

    _controls_index.json_: прежде всего надо добавить в раздел ALL, а затем добавить в нужные разделы в зависимости от type и category оффера.
    В нашем случае это RENT_APARTMENT, RENT_ROOMS, RENT_HOUSE (число - это ссылка на наш параметр по номеру, начиная с 0).


17. Унификация офферов
    * Так как переунификацией теперь занимается унифаер (вместо реиндексера) появилась возможность с меньшим риском выкатывать код унификации, который изменит хэши у большого кол-ва офферов (например, добавить новое поле для всех офферов).
    Раньше для безопасной выкатки такого кода (чтобы не забивать очередь realty-unified-offers) использовались depletion фичи.
    Теперь есть возможность регулировать переунификацию следующими фичами:
* - reunify_rps - % от дефолтного rps переунификации (например 10 означает 10%)
* - skip_reunify - пропускаем обработку сообщений переунификации

## Какие сервисы затрагивает
* partnerdata-feedloader
* realty-feed-processor
* realty-vos-consumer
* realty-vos-scheduler
* realty-vos-api
* realty-indexer
* realty-reindexer
* realty-searcher
* realty-gateway
