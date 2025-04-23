# MbiPartner
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/).

Данные в стейте:

```
{
    "auction": "",
    "delivery": {
        regionGroupId: "kadavr_mock_default_region_group_id",
    },
    "apiLog": "",
    "reports": [],
}
```

## auctionBulkOfferBids
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/auctionBulkOfferBids/).

Возвращает ровно то, что передали (данные в XML формате)

## saveRegionsGroup
[Документация](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/editregiondeliverygroup/).

Возвращает id группы регионов, который передали плюс валюту RUR и статус группы NEW. Если id группы не передан, берет его из стейта из delivery.regionGroupId

## getApiResources
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/apiResources/).

Возвращает ветку apiResources из стейта (список ресурсов api)

## viewApiLog
@deprecated: use MbiLogProcessor.getPushApiLogs https://st.yandex-team.ru/MARKETPARTNER-17452
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/viewCpaApiLog/).

Возвращает ветку apiLog из стейта (список логов запросов пуш апи и пулл апи)

## commitPassport
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/commitPassport/).
Параметры запроса: /confirm/commit.

+ **digest** - уникальный идентификатор, генерируемый при создании ссылки-приглашения в партнерский интерфейс
    для пользователя;
+ **confirm** - может принимать только одно значение - строку 'process'. Переводит запрос в режим либо принятия,
  либо отказа от приглашения;
+ **commit** - может принимать только одно значение - строку 'yes'.

В зависимости от переданных параметров возвращает:
+ без параметров: ошибку (BAD_PARAM_TO_CALL);
+ **digest**: запрос только с этим параметром вернет пустой массив result (при успешном выполнении)
  или ошибку при попытке использовать чужую ссылку (wrong_user),
  ошибку при попытке воспользоваться ссылкой дважды (no_such_digest);
+ **digest** и **confirm='process'**: отказ от приглашения;
+ **digest**, **confirm='process'** и **commit='yes'**: принятие приглашения;

Пример ответа при успешном принятии приглашения:
```
{
    result: [{ value: 'YES'}]
}
```
## enableFeature
[Документация](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/enablefeature/).

Если программа была в состоянии  FAIL или  DONT_WANT , включает программу/возвращает на модерацию (переводит в статус  NEW или  SUCCESS , если программа не требует премодерации).
В случае успеха возвращает новый статус, аналогично вызову /featureInfo следом.

## cpcstate
[Документация](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/cpcstate/).

Ручка возвращает актуальное состояние подключения магазина к программе "Покупка на сайте". Ручка работает в json-формате.

## getCampaignProgramsState
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/get-campaigns-program/).

Получение статуса по указанной программе или всем программам магазина.

## getCampaignFullInfo
[Документация](https://swagger.market.yandex-team.ru/#/campaign-controller/searchFullCampaignInfosUsingGET/).

Ручка для получения информации по всем поставщикам клиента.

## getCampaignProgramState
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/get-campaigns-program/).

Получение статуса по указанной программе.

## getCampaignFinanceInfo
[Документация](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/getcampaignfinanceinfo/).

Получение информации о финансовом положении магазина.

## manageParam
[Документация](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/manageParam/)

Получает/меняет значения переданных параметров.

## getCampaignSteps
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/wizard/).

Получает текущие шаги визардов Белого и Синего (дропшипы).

## getCampaignStep
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/wizard/).

Получает информацию о заданном шаге визардов Белого и Синего (дропшипы).

## getReports
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/get-reports/).

Возвращает все отчёты партнёра из стейта:
```
[
    {
        id: 'id',
        partnerId: 10217455,
        reportType: 'FULFILLMENT_ORDERS',
        requestCreatedAt: '2019-11-14T14:27:26.120658+03:00',
        state: 'DONE',
        stateUpdatedAt: '2019-11-14T14:27:27.24016+03:00',
        urlToDownload: '1c46d960-124a-46c6-813b-574db6716170.xlsx',
    },
]
```

## getIndexingReportSummary
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/indexing-report-controller/getFeedIdxSummaryUsingGET).

Получить информацию по последним результатам индексации всех фидов магазина.

## revokeYMLClaim
[Документация](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/revokeYMLClaim/).

Снять отключение за YML.

## getIndexingFeedFileUrl
[Документация](https://swagger.market.yandex-team.ru/#/indexing-report-controller/getFeedFromArchiveUsingGET).

Получить ссылку на фид из архива версий. Версия фида, которая была на момент скачивания.

## getIndexingFeedFullHistory
[Документация](https://swagger.market.yandex-team.ru/#/indexing-report-controller/getFullHistoryUsingGET).

Получить историю полных индексаций прайс-листа.

## getIndexingFeedDiffHistory
[Документация](https://swagger.market.yandex-team.ru/#/indexing-report-controller/getDiffHistoryUsingGET).

Получить страницу истории изменения цен прайс-листа

## getIndexingFeedDetails
[Документация](https://swagger.market.yandex-team.ru/#/indexing-report-controller/getFeedLogErrorsUsingGET).

## getOrdersGET
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/orders-controller-v-2/getOrdersUsingGET_1).

Получить список заказов

## getOrdersCountByStatusesGET
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/orders-controller-v-2/getOrdersCountByStatusesUsingGET_1).

Получить информацию по количеству заказов по статусам

## getContracts
[Документация](https://swagger.market.yandex-team.ru/#/supplier-contract-controller/getContractsUsingGET).

Получение информации о выплатах по договорам

## getOrderSummaryV2
[Документация](https://swagger.market.yandex-team.ru/#/supplier-summary-controller/getOrderSummaryInfoV2UsingGET).

Получение сводки по заказам поставщика

## getShopSkuUsingGET
[Документация](https://swagger.market.yandex-team.ru/#/mapping-controller/getShopSkuUsingGET).

Получить информацию об офере и его привязкам по Shop SKU

## updateOfferProcessingStatusUsingPUT
[Документация](https://swagger.market.yandex-team.ru/#/mapping-controller/updateOfferProcessingStatusUsingPUT).

Изменить статус процессинга офера для ShopSKU

##getFeeds
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/getFeeds/).

Получить список фидов магазина

## feeds
[Документация](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/feed-controller/getFeedsGETUsingGET/).

Получить список фидов магазина

## deleteReport
[Документация](https://swagger.market.yandex-team.ru/#/async-reports-controller-v-1/deleteReportUsingDELETE).

Удалить отчет по его id

## bindTelegram
[Документация](https://swagger.market.yandex-team.ru/#/telegram-controller/bindAccountUsingPOST).

Подключить уведомления в телеграм

## unbindTelegram
[Документация](https://swagger.market.yandex-team.ru/#/telegram-controller/deleteAccountUsingDELETE).

Отключить уведомления в телеграм

## getTelegramBind
[Документация](https://swagger.market.yandex-team.ru/#/telegram-controller/getUsersUsingGET).

Получить список пользователей, подключивших уведомления

## getReceptionTransferAct
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/orders-controller-v-2/getReceptionTransferActUsingGET_1)

Скачивание акта приема-передачи

## getCampaignsOfferMappingShopSkus
[Документация](https://swagger.market.yandex-team.ru/#/mapping-controller/getShopSkusUsingGET)

Получение списка shop-sku

## getCampaignsOfferMappingShopSkusPOST
[Документация](https://swagger.market.yandex-team.ru/#/mapping-controller/getShopSkusUsingPOST)

Получение списка shop-sku

## getPointSwitchStateUsingGET
[Документация](https://swagger.market.yandex-team.ru/#/logistic-partner-controller/getPointSwitchStateUsingGET)

Получение сведений о предыдущем складе для отгрузки товаров

## getPaymentOrders
[Документация](https://swagger.market.yandex-team.ru/#/payment-order-controller/getPaymentOrdersUsingGET)

Получение номеров платежных поручений

## pushReadyForTesting
[Документация](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/pushReadyForTesting/)

Отправка магазина на проверку

## cpaTestingReadyIndex
[Документация](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/cpatestingreadyindex/)

Получение состояния доступного индекса

## loadFeedsToSandbox
[Документация](https://swagger.market.yandex-team.ru/#/sandbox-controller/loadFeedsToSandboxUsingPOST)

Загрузка фида в песочницу

## getDocumentsMeta
[Документация](https://swagger.market.yandex-team.ru/#/document-controller/getDocumentsMetaUsingGET)

Получение информации по документам за указанный период

## getSubsidyDocumentsStatuses
[Документация](https://swagger.market.yandex-team.ru/#/document-controller/getSubsidyDocumentsStatusesUsingGET)

Получение статуса субсидийных документов за год

## getOutcomeActsByYears
[Документация](https://swagger.market.yandex-team.ru/#/document-controller/getSubsidyDocumentStatusesByYearsUsingGET)

Получение статусов субсидийных документов за все года

## getPlacementStatus
[Документация](https://swagger.market.yandex-team.ru/#/partner-placement-controller/getPartnerPlacementStatusUsingGET)

Получение статуса (включен/выключен) магазина/поставщика.

## setPlacementStatus
[Документация](https://swagger.market.yandex-team.ru/#/partner-placement-controller/changePartnerPlacementStatusUsingPOST)

Выставление статуса (включен/выключен) магазина/поставщика.

## getCampaignsOfferMappingShopSkusLowStocksPOST
[Документация](https://swagger.market.yandex-team.ru/#/stocks-lack-controller/getShopSkusWithLowStocksUsingPOST)

Получение списка shopSku с заканчивающимися стоками

## supplierPromoOffersCommit
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/promo-xlsx-controller/commitPromoOffersUsingPOST)

Подтверждение участия офферов в акции

## supplierPromoOffersUpload
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/promo-xlsx-controller/validatePromoOffersUsingPOST)

Начать валидацию офферов для участия в акции

## supplierPromoOffersGetUploadInfo
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/promo-xlsx-controller/getPromoOffersValidationInfoUsingGET)

Получить информацию о статусе валидацииы

## postSupplierPromoOffers
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/promo-pi-controller/updatePromoOffersUsingPOST)

Обновить статусы и параметры участия офферов в акции

## getShopDailyOrderSummary
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/partner-summary-controller/getShopOrderSummaryDailyInfoUsingGET)

Получение сводки по заказам DBS-партнера за последнюю неделю

## getTplOutletPartners
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/tpl-partner-controller/getPartnersUsingGET_3)

Получение списка tpl-partners существующих на аккаунте

## getOrdersInfo
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/orders-shipment-info-controller/getOrdersInfoUsingGET)

Получить информацию о валидных и невалидных заказах для генерации ярлыков

## uploadFeedEkat
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/file-controller/uploadFeedUsingPOST)

## validateFeedEkat
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/united-feed-validation-controller/validateUsingPOST_2)

## getFeedValidationEkat
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/united-feed-validation-controller/validateUsingGET)

## getPartnerUserSurveysActiveInUi
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/periodic-survey-controller/getPartnerUserSurveysActiveInUiUsingGET)

Получить опросы (пока не должно быть > 1) по магазину для пользователя, которые уже можно показывать в UI (не просто активные, а пролежавшие активными сутки после создания или после того как опрос отложили)

## getPartnerUserSurveyById
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/periodic-survey-controller/getPartnerUserSurveyByIdUsingGET)

Получить опрос по ссылке в письме (по идентификатору)

## answerSurvey
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/periodic-survey-controller/answerSurveyUsingPOST)

Отправить ответы на опрос

## getOrderItemsDetails
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/orders-controller-v-2/getOrderItemsDetailsUsingGET)

Получить разбивку по статусам для каждой штуки товара для заказа

## updateBusinessWarehouse
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/business-warehouse-controller/updateBusinessWarehouseUsingPUT)

Сохраняет настройки DBS-склада

## getBusinessWarehouses
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/business-warehouse-controller/getBusinessWarehousesUsingGET)

Получает список складов бизнеса

## getCutoffMessages
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/partner-cutoff-controller/getCutoffMessagesUsingGET)
Получение списка отключений и связанных с ними сообщений.

## getReadyToPickupSortingCenters
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/resupply-controller/getReadyToPickupSortingCentersUsingGET)

Получение списка сортировочных центров, готовых для самовывоза

## getPremoderationCloseCutoffsManual
[Документация](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/premoderation-controller/closeManualCutoffsUsingGET)

Снимает ручные катоффы с магазина

## showMissedDatasourceInfo
[Документация](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/showmisseddatasourceinfo)

Возвращает набор незаполненных полей о магазине

## getPromoLastValidationsInfo
[Документация](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/supplier-promos-controller/getPromoValidationsInfoByIdUsingPOST)

Получение последних успешных валидаций файлов по акциям.

## getPromoOrdersInfo
[Документация](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/supplier-promos-controller/getPromoOrdersInfoByIdUsingPOST)

Получение заказов по акциям. Возвращаются заказы только по партнерским акциям.

## getStandardCashback
[Документация](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/partner-standard-cashback-controller/getStandartCashbackUsingGET)

Получение описания стандартной акции

## getLoyaltyProgram
[Документация](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/loyalty-information-controller/getLoyaltyInformationUsingGET)

Получение информации об участии партнера в программе лояльности

## genericStandardPromos
[Документация](http://market-loyalty.tst.vs.market.yandex.net:35815/swagger-ui.html#/partner-cashback-controller/getPartnerStandardStandardPromosUsingGET)

Информация по стандартным партнерским промкам

## getCustomCashback
[Документация](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/partner-custom-cashback-controller/getCustomCashbackUsingGET)

Получение списка кастомных акций с пагинацией

## createCustomCashback
[Документация](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/partner-custom-cashback-controller/createCustomCashbackUsingPOST)

Создание кастомной акции

## deleteCustomCashback
[Документация](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/partner-custom-cashback-controller/deleteCustomCashbackUsingDELETE)

Удаление кастомной акции

## deleteCampaign
[Документация](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/campaign-controller/deleteCampaignUsingDELETE)

Удаление магазина
