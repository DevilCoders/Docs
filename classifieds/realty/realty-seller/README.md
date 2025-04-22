Распродажи и цены на размещения и ВАСы:
==============

На данный момент в недвижимости существует несколько механизмов оплаты услуг: для физиков, для криков и автопродление. Все они каким-то образом получают актуальные цены для продуктов.

Технически пайплайн оплаты можно разделить на 2 категории - ручная оплата (realty3-api -> seller-api -> vos2-api + abram -> seller-api) и автоматический (seller-scheduler | seller-consumer -> vos2-api + abram).
В части получения цен механизм один и тот же, кроме случаев с автопродлением. О них ниже.

##Цены

Цены хранятся в виде ценовых матриц в realty-abram (verba.export.xml - цены на размещение и ВАСы, call_price_lists_extended.xml и call_price_lists_maximum.xml -  тарифы на звонки). 
В пайплайне ручной оплаты для физиков цены участвуют в следующих ручках апи:

http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/Products/calculateProductPricesBatchRoute
http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/Products/calculateProductPricesByParamsRoute
http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/Products/initPurchase

В seller-api:
http://realty-seller-api-main.vrts-slb.test.vertis.yandex.net/swagger/#!/product/calculateProductPricesBatchRoute
http://realty-seller-api-main.vrts-slb.test.vertis.yandex.net/swagger/#!/product/calculateProductPricesByParamsRoute
http://realty-seller-api-main.vrts-slb.test.vertis.yandex.net/swagger/#!/purchase/initPurchaseRoute

В абрам 
http://realty-abram-api.vrts-slb.test.vertis.yandex.net/swagger/#!/prices/getPricesForOfferParams (технически, эта ручка дергает getBatchPricesForOfferParams)
http://realty-abram-api.vrts-slb.test.vertis.yandex.net/swagger/#!/prices/getBatchPricesForOfferParams

Механизм получения цен всегда одинаковый, его расписывать не имеет смысла:

##Скидки

К модификаторам цен относятся скидки и промокоды (ru.yandex.realty.seller.model.product.PriceModifier)
Скидочные модификаторы цен применяются в абраме исходя из текущих условий распродажи, промокоды применяются в селлере после запроса в promocoder.

На текущий	 момент использовались 3 вариации распродаж:
На размещение для физических лиц,
На ВАСы для физических лиц,
На размещение офферов на аренду квартир в МСК и МО для агентов.

Важно, условия распродажи должны проверяться в двух местах (до появления полноценного price-сервиса):
Realty3-api, ручка check-discount - используется для отображения баннеров.
ru.yandex.realty.abram.managers.AvailabilityManager в абрам для применения самой скидки.

Размер скидки рассчитывается в процентах и абсолютной величине, в дальнейшем для расчетов используется именно абсолютная величина.
Применение скидки в ручках запросов цен здесь ru.yandex.realty.seller.service.impl.PriceCalculator#applyDiscountsAndConvert
Применение скидок в общем PriceContext для расчета стоимости по офферу или батчу запросов здесь ru.yandex.realty.seller.service.impl.PriceCalculator#applyFeaturesToPriceContext 

##Как сделать новую скидку

Сейчас для запуска новых скидок по уже существующим критериям достаточно ~~дождаться полноценного прайс сервиса~~ поменять даты начала и окончания скидок:
В апи ru.yandex.realty.abram.managers
в селлере ru.yandex.realty.managers.users.PersonalAccountUsersManager

Для новых скидок нужно добавить новые даты в вышеуказанные места, расширить прото-модель ApiNeedShowDiscountResponse и применить скидки в абраме по заданным критериям.

##Автопродление
При автопродлении цены формируются так же, как и при первоначальной покупке, но модификаторы цен полностью или частично удаляются тут:
ru.yandex.realty.seller.processing.products.CreateRenewedProductStage.preparePriceContext

Сейчас для размещений остаются только модификаторы скидлок, удаляются промокоды. Для всех остальных случаев модификаторы удаляются полностью. Это тоже нужно учитывать при разработке новых распродаж.

