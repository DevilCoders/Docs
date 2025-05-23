## Тесты
Тесты на импорт логов разбиты на два типа: тесты с локальным YT и
тесты map/reduce операций без использования YT (поведение YT эмулируется).
Второй тип тестов сделан чтобы можно было проверить результаты на каждом
этапе импорта отдельно.
# Тесты с локальным YT
Файл `yt_test.py`.
Входные данные для локального YT лежат в папке cypress_dir. При необходимости
можно сгенерировать новые входные таблицы при помощи утилиты
`arcadia/quality/ytlib/tools/renamer`.
Пример запуска:
```
./yt_renamer -i //home/maps/automotive/tests/canon_data/2020-03-16 -o - --infer --strict --for-scan --sample 0 --sb APIKey --sb  EventType --sb  EventName --sb  DeviceID --sb  EventTimestamp
```
В файле отдельный тест сделан для проверки существования входных таблиц,
а так же по тесту на каждую таблицу с канонизацией результата через
`ya make -ttt --canonize-tests`.
# Тесты с эмуляцией YT
Файл `log_test.py`.
Внутри теста есть небольшой framework имитирующий работу YT, он лежит в классе
`Data`. Конструктор принимает на вход `list` таблиц, каждая из которых - `list`
строк в формате `dict` без кодировки (все строки типа `bytes`, так как в импорте
все операции `format=yt.YsonFormat(encoding=None)`). Входные данные
для этого теста лежат в папке `data` и могут быть сгенерированы YQL запросом
вида
```
use hahn;

$list_to_string = ($list) -> {
    RETURN CAST(Yson::SerializeJson(Yson::From($list)) AS String);
};

select
    `ADVID`,
    `APIKey`,
    `APIKey128`,
    `AccountID`,
    `AccountType`,
    `Age`,
    `AndroidID`,
    `AppBuildNumber`,
    `AppDebuggable`,
    `AppFramework`,
    `AppID`,
    `AppPlatform`,
    `AppVersionName`,
    `AttributionID`,
    `AttributionIDChanged`,
    `AttributionIDUUIDHash`,
    `CellID`,
    `ChargeType`,
    `ClickDate`,
    `ClickDateTime`,
    `ClickTimestamp`,
    `ClientIP`,
    `ClientIPHash`,
    `ClientKitVersion`,
    `ClientPort`,
    `ConnectionType`,
    `CountryCode`,
    `CrashBinaryName`,
    `CrashDecodedEventValue`,
    `CrashEncodeType`,
    `CrashFileName`,
    `CrashGroupID`,
    `CrashID`,
    `CrashMethodName`,
    `CrashReason`,
    `CrashReasonMessage`,
    `CrashSourceLine`,
    `CrashThreadContent`,
    `CryptaID`,
    `DecodeErrorDetails`,
    `DecodeGroupID`,
    `DecodeRequiredSymbolsId`,
    `DecodeStatus`,
    `DecodeTimestamp`,
    `DeduplicationEnabled`,
    `DeviceID`,
    `DeviceIDHash`,
    `DeviceIDSessionIDHash`,
    `DeviceType`,
    `EcommerceCartItemPriceFiatUnitType`,
    `EcommerceCartItemPriceFiatValue`,
    `EcommerceCartItemQuantity`,
    `EcommerceOrderId`,
    `EcommerceOrderIdHash`,
    `EcommerceOrderPayloadTruncatedPairsCount`,
    `EcommerceProductActualPriceFiatUnitType`,
    `EcommerceProductActualPriceFiatValue`,
    `EcommerceProductCategoryPath1`,
    `EcommerceProductCategoryPath10`,
    `EcommerceProductCategoryPath2`,
    `EcommerceProductCategoryPath3`,
    `EcommerceProductCategoryPath4`,
    `EcommerceProductCategoryPath5`,
    `EcommerceProductCategoryPath6`,
    `EcommerceProductCategoryPath7`,
    `EcommerceProductCategoryPath8`,
    `EcommerceProductCategoryPath9`,
    `EcommerceProductName`,
    `EcommerceProductOriginalPriceFiatUnitType`,
    `EcommerceProductOriginalPriceFiatValue`,
    `EcommerceProductPayloadTruncatedPairsCount`,
    `EcommerceProductSku`,
    `EcommerceReferrerId`,
    `EcommerceReferrerType`,
    `EcommerceScreenCategoryPath1`,
    `EcommerceScreenCategoryPath10`,
    `EcommerceScreenCategoryPath2`,
    `EcommerceScreenCategoryPath3`,
    `EcommerceScreenCategoryPath4`,
    `EcommerceScreenCategoryPath5`,
    `EcommerceScreenCategoryPath6`,
    `EcommerceScreenCategoryPath7`,
    `EcommerceScreenCategoryPath8`,
    `EcommerceScreenCategoryPath9`,
    `EcommerceScreenName`,
    `EcommerceScreenPayloadTruncatedPairsCount`,
    `EcommerceScreenSearchQuery`,
    `EcommerceType`,
    `ErrorGroupID`,
    `ErrorID`,
    `EventBytesTruncated`,
    `EventDate`,
    `EventDateTime`,
    `EventEnvironment`,
    `EventFirstOccurrence`,
    `EventGlobalNumber`,
    `EventGroupCount`,
    `EventGroupID`,
    `EventGroupIDHash`,
    `EventGroupIndex`,
    `EventID`,
    `EventIsTruncated`,
    `EventName`,
    `EventNumber`,
    `EventNumberOfType`,
    `EventSource`,
    `EventTimeOffset`,
    `EventTimeZone`,
    `EventTimestamp`,
    `EventType`,
    `EventValue`,
    `EventValueCrash`,
    `EventValueError`,
    `EventValueJsonReference`,
    `EventValueReferrer`,
    `IFV`,
    `IFVHash`,
    `InvalidationTimestamp`,
    `IsCandidateForThirdPartyClicklog`,
    `IsEventForProfileUpdate`,
    `IsExtraLocationEvent`,
    `IsInstallationTrackingEnabled`,
    `IsOwnedByYandex`,
    `IsProfileEventForReports`,
    `IsReengagement`,
    `IsRevenueVerified`,
    `IsRooted`,
    `KitBuildNumber`,
    `KitBuildType`,
    `KitVersion`,
    `LimitAdTracking`,
    `Locale`,
    `LocationSource`,
    `LogfellerTimestamp`,
    `Manufacturer`,
    `Model`,
    `NetworkType`,
    $list_to_string(`NetworksInterfaces_Macs`) AS `NetworksInterfaces_Macs`,
    $list_to_string(`NetworksInterfaces_Names`) AS `NetworksInterfaces_Names`,
    `OAID`,
    `OSApiLevel`,
    `OSBuild`,
    `OSVersion`,
    `OpenType`,
    `OperatingSystem`,
    `OperatorID`,
    `OperatorName`,
    `OriginalDeviceID`,
    `OriginalManufacturer`,
    `OriginalModel`,
    `ProfileAttributeVersion`,
    `ProfileID`,
    `ProfileIDHash`,
    `PublisherID`,
    `PushActionID`,
    `PushActionIDString`,
    `PushActionType`,
    `PushCampaignID`,
    `PushChanged`,
    `PushCorrelationID`,
    `PushEnabled`,
    `PushErrorCategory`,
    `PushErrorDetails`,
    `PushGroupID`,
    `PushHypothesisID`,
    `PushIosAlertEnabled`,
    `PushIosBadgeEnabled`,
    `PushIosSoundEnabled`,
    `PushMessageID`,
    `PushMessageLanguage`,
    `PushSentTimestamp`,
    `PushSystemNotifyTimestamp`,
    `PushTag`,
    `PushToken`,
    `PushTokenType`,
    `PushTransferID`,
    `ReceiveDate`,
    `ReceiveTimestamp`,
    `ReferrerClickTimestamp`,
    `ReferrerInstallationBeginTimestamp`,
    `RegionID`,
    `RegionTimeZone`,
    $list_to_string(`ReportEnvironment_Keys`) AS `ReportEnvironment_Keys`,
    $list_to_string(`ReportEnvironment_Values`) AS `ReportEnvironment_Values`,
    `RequestID`,
    `RevenueCurrency`,
    `RevenueOrderId`,
    `RevenueOrderIdHash`,
    `RevenueOrderIdSource`,
    `RevenuePrice`,
    `RevenueProductId`,
    `RevenueQuantity`,
    `RevenueReceiptData`,
    `RevenueReceiptSignature`,
    `RevenueReceiptTransactionId`,
    `RevenueValidationEnvironment`,
    `ScaleFactor`,
    `ScreenDPI`,
    `ScreenHeight`,
    `ScreenWidth`,
    `SendIDHash`,
    `SendTimeZone`,
    `SendTimestamp`,
    `SessionID`,
    `SessionType`,
    `Sex`,
    `Sign`,
    `StartDate`,
    `StartTime`,
    `StartTimeCorrected`,
    `StartTimeObtainedBeforeSynchronization`,
    `StartTimeZone`,
    `StartTimestamp`,
    `SupPushID`,
    `SupPushType`,
    `TokenEnvironment`,
    `TrackingID`,
    `UUID`,
    `UUIDHash`,
    `UrlHost`,
    `UrlPath`,
    `UrlScheme`,
    `Version`,
    `WifiAccessPointSsid`,
    `WifiAccessPointState`,
    `WindowsAID`,
    `XivaEvent`,
    `XivaTransitID`,
    `YMTrackingID`,
    `_logfeller_index_bucket`,
    `_logfeller_timestamp`,
    `_stbx`,
    `iso_eventtime`,
    `source_uri`
from `//logs/appmetrica-yandex-events/1d/2020-03-16`
where APIKey in (517964, 517959,
                 2940673,
                 2950450,
                 2977624,
                )
and DeviceID in ('d66806f64dec0fc1575c491429a0e158', '79ee80f973ec5710b8f3387531cbc013');
```
с выгрузкой результата в формате json.
После этого выполните преобразование файла с помощью скрипта patch_lists.py

Класс `Data` на данный момент поддерживает операции
* `map(self, mapper)`,
* `reduce(self, reducer, reduce_by: list, with_context: bool)`, где reduce_by -
список полей, по которым делать reduce, а with_context - нужен ли операции
`reducer` параметр `context` (поддерживается только `table_index`),
* `sort(self, sort_by: list)`, где `sort_by` - список полей, по которым сортируем,
* `result(self)` - возвращает `list` выходных таблиц.
Тест повторяет все операции, которые производятся в `import_logs.py` с
использованием тех же map/reduce функций, но объектом `Data` вместо `yt.wrapper`.
При изменении алгоритма импорта алгорим в этом тесте так же необходимо обновить.
В файле создан отдельный тест на каждый этап импорта логов с канонизацией
результата через `ya make -ttt --canonize-tests`.
