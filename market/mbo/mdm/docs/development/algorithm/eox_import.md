# Импорт серебра SSKU из ЕОХ (Datacamp)

Партнёрские данные о товарах приходят в МДМ из Единого Офферного Хранилища (ЕОХ). Наш сервис регулярно читает эти данные в асинхронном режиме и сохраняет как Серебро SSKU. То есть это "сырые" данные, из которых мы потом другими процессами сварим более качественную запись про SSKU. В данном разделе рассмотрим алгоритм непосредственного импорта сырых данных из ЕОХ.

**Вход алгоритма импорта**

- Набор офферов из ЕОХ в сыром бинарном прото-формате

**Выход алгоритма импорта**

- Отбрасывание ненужных неподдерживаемых офферов
- Сохранение поддерживаемых офферов, преобразованных во внутренний формат
- Разметка удаленных офферов
- Сохранение служебной информации (миграции, бизнес-группы и прочее, рассмотрим ниже)
- Пополнение очереди рассчётов SSKU для дальнейшего вычисления золотых записей на основе свежего серебра

## Формат хранилища

*TL;DR:*

 - [Протобуфка](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/UnitedOffer.proto)

 - [Конвертёр в коде](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/masterdata/services/param/MdmFromDatacampConverter.java)

### UnitedOffer.proto

В ЕОХ офферы хранятся в Yt-таблицах в виде прото-сообщений [UnitedOffer.proto](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/UnitedOffer.proto).

```protobuf
message UnitedOffer
{
    // Базовый оффер
    optional Offer basic = 1;

    // Сервисные офферы по shop_id
    // shop_id -> service offer
    map<uint32, Offer> service = 2;

    ...
}
```

Сообщение представляет собой [бизнес-оффер](../../contour/business_domain/business_offer.md#business_offer). Внутри сообщения `Offer` лежит огромное количество полей, из которых нам чаще всего нужны только следующие:

```protobuf
message Offer
{
    // Идентификация офера
    optional OfferIdentifiers      identifiers      = 1;
    // Метаинформация про офер и его части
    optional OfferMeta             meta             = 2;
    // Статусы офера во всех пайплайнах
    optional OfferStatus           status           = 4;
    // Описание товара
    optional OfferContent          content          = 5;
}
```

Поля `OfferIdentifiers`, `OfferMeta` и `OfferStatus` используются нами в служебных целях, а вот самая интересная начинка с партнёрскими данными находится в `OfferContent`.

```protobuf
message OfferContent
{
    // Характеристики товара, полученные от партнера
    optional PartnerContent     partner          = 1;

    // Золотая запись, которую мы записываем в ЕОХ в самом конце наших пайплайнов.
    // В процессе импорта никак не задействована, однако полезно увидеть её здесь.
    optional MarketMasterData   master_data      = 8;
}
```

В поле `PartnerContent` нас интересует то, что поставщик вбивал в своём личном кабинете в ПИ для данного товара:

```protobuf
message PartnerContent
{
    optional OriginalSpecification     original             = 20;
    optional OriginalTerms             original_terms       = 22;
}
```

И вот уже в этих полях лежат конкретные чиселки и строчечки, которые партнёр вводил в ПИ и которые нам так нужны. Для примера посмотрим на `OriginalSpecification`:

```protobuf
message OriginalSpecification
{
    optional StringListValue country_of_origin = 19;
    optional PreciseWeight weight         = 20;
    optional PreciseDimensions dimensions = 21;
}
```

На самом деле полей там значительно больше, но данном примере видно поля с ВГХ и страной производства. Парсинг этих и других полей происходит в [прото-конвертёре](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/masterdata/services/param/MdmFromDatacampConverter.java) старого МДМ. Результат конвертации генерит бизнес-оффер в нашем внутреннем параметрическом формате `CommonSsku`, с которым мы уже умеем работать.

### Подписки на поля

В протобуфке помимо самих полей указывается также дополнительная разметка примерно в таком виде:

```protobuf
message SomeOfferData
{
    optional Data important_value = 19
    [ (Market.mdm_subscriber) = ST_TRIGGER ];
    optional Data useful_value = 20
    [ (Market.mdm_subscriber) = ST_SHIPMENT ];
    optional Data ignorable_data = 21;
}
```

Эта разметка указывает, в каком режиме ЕОХ будет посылать нам эти данные. Чаще всего мы используем подписку одного из двух видов:

- ST_SHIPMENT - размеченное поле будет отправлено к нам в составе прото-сообщения. При этом изменение этого поля внутри Хранилища **не инициирует** отправку оффера в МДМ. Такая подписка хороша для nice-to-have атрибутов, которые в целом полезные, но не основополагающие для наших процессов.
- ST_TRIGGER - размеченное поле будет отправлено к нам в составе прото-сообщения. Более того, любое изменение этого поля инициирует отправку оффера к нам в МДМ (включая все SHIPMENT-поля). Такая подписка хороша для существенных атрибутов, изменения в которых требуют полноценной обработки всего оффера. Почти все партнёрские данные размечены именно так.

Отсутствие нашей подписки на поле означает, что это поле ничего не инициирует и никогда к нам не придёт. А при парсинге протобуфки там всегда будет пустота или дефолтное протобуфное неинициализированное значение.

В примере выше, если в `SomeOfferData` любым образом поменяется `important_value`, то к нам тут же прилетит сообщение `SomeOfferData`, содержащее свежие `important_value` и `useful_value`. Если поменяется `useful_value`, то ничего не произойдёт. А значение `ignorable_data` мы вообще никогда в жизни не увидим, т.к. оно вообще ничем не размечено и не будет входить в прото-сообщение.

{% note warning %}

Используйте подписку ST_TRIGGER с ВЕЛИЧАЙШЕЙ осторожностью. Некоторые поля оффера меняются в тысячи раз чаще, чем другие. Подписка на флапающий атрибут в режиме триггера может привести к потопу из ЕОХ в сторону МДМ, т.к. каждое изменение такого поля будет инициировать переотправку.

{% endnote %}

Чуть подробнее от команды Хранилища про подписки написано в комментарии [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/common/extension.proto?rev=r9405994#L11-15).

## Интеграция, транспорт, метрики

Для общения между ЕОХ и МДМ используется асинхронная очередь сообщений Logbroker. Конкретно для импорта серебра SSKU мы используем топики в инсталляции `logbroker` по следующим путям:

- [market-indexer/testing/united/datacamp-offers-to-mdm](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-offers-to-mdm) - в деве и тестинге
- [market-indexer/prod/united/datacamp-offers-to-mdm](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-to-mdm) - в проде

ЕОХ непрерывно в режиме онлайн записывает в эти топики свежие изменения офферов в прото-формате

```protobuf
message UnitedOffersBatch
{
    repeated Market.DataCamp.UnitedOffer offer = 1;
}
```

В старом МДМ эти топики непрерывно считываются консьюмерами. Удобная точка входа находится в классе [DataCampToMdmLogbrokerMessageHandler](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/infrastructure/logbroker/DataCampToMdmLogbrokerMessageHandler.java). Поскольку и писатель, и читатель асинхронные, обмен данными происходит постоянно и в идеале бесперебойно. Это принципиально отличается от синхронного обмена данными через ручки (эндпоинты APIшек).

**Краткая схема и особенность нашего чтения из Логброкера**

1. Через библиотечный консьюмер-клиент вычитываем сообщение из топика. Это происходит вне транзакций.
2. Парсим набор ключей оффера из сообщения.
3. Парсим сами офферы из сообщения и пробуем их импортировать.
  3.1. Если всё прошло успешно, то коммитим чтение данного сообщения в Логброкер
  3.2. Если импорт не состоялся, то укладываем ключики из шага (2) в специальную fail-очередь для последующего перезапроса. А затем *всё равно коммитим транзакцию* чтения из Логброкера.

Такая хитрая схема нужна для обхода несовершенства клиента Логброкера, когда выброшенное в пределах транзакции исключение могло прибить весь клиент до следующего рестарта приложения.

**Графики**

Следить за общим потоком офферов из ЕОХ в МДМ можно на [графике](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_writeSession&graph=auto&Account=market-indexer&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=BytesWritten%2A&TopicPath=market-indexer%2Fprod%2Funited%2Fdatacamp-offers-to-mdm&Topic=%21total&Producer=%21total&b=7d&e=):

<iframe height="400" width="100%" frameborder="0" src="https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_writeSession&graph=auto&Account=market-indexer&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=BytesWritten%2A&TopicPath=market-indexer%2Fprod%2Funited%2Fdatacamp-offers-to-mdm&Topic=%21total&Producer=%21total&b=7d&e="></iframe>

По оси Y указана нагрузка на топик в байтах. Это не поможет понять точное число сообщений, но позволит сравнительно прикинуть текущую нагрузку в сравнении с фоновой, были ли пики или просадки.

Метрики чтения из топика нашим клиентом можно посмотреть на нашем [дашборде](https://grafana.yandex-team.ru/d/EyppVEZnk/datacamp-mdm-logbroker?orgId=1&refresh=10s):

<iframe height="650" width="100%" frameborder="0" src="https://grafana.yandex-team.ru/d/EyppVEZnk/datacamp-mdm-logbroker?orgId=1&refresh=10s&kiosk"></iframe>

## Алгоритм импорта

Точка входа класс [DatacampOffersImporterImpl](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/datacamp/DatacampOffersImporterImpl.java), метод `importOffers`.

**0. Конвертация сырых данных**
Точка входа [MdmFromDatacampConverter](https://a.yandex-team.ru/arcadia/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/masterdata/services/param/MdmFromDatacampConverter.java)

Конвертируем поля из прото формата Datacamp во внутренний формат.

Ниже представлена логика для "особенных" полей:
- **Флаг удаления оффера** - флаг, указывающий на то, что оффер удален из ЕОХ, в протобуфке лежит [тут](https://a.yandex-team.ru/svn/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto#L231)

**1. Первичная фильтрация офферов**

Точка входа [DatacampOffersFiltrator](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/datacamp/DatacampOffersFiltrator.java), метод `filterAllowedEkatOffers`. На вход приходят расконвертированные прото-офферы в сыром, но уже внутреннем формате.

1. Прогружаем из [Key-Value](../practices/skv.md) список запрещённых `business_id`. Это подхак для отбрасывания сверхтяжёлых поставщиков, которые МДМ не поддерживает. В нормальной ситуации этот набор должен быть пустым.
2. Если оффер не имеет сервисов (ни у нас в БД, ни в пришедшем бизнес-оффере), то отбрасываем его.

Во всех остальных случаях оффер уходит на дальнейшую обработку.

**2. Вторичная фильтрация офферов**

Точка входа [DatacampOffersFiltrator](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/datacamp/DatacampOffersFiltrator.java), метод `filterOffersOfNonMdmCompatibleSuppliers`.

Выбрасываем из оффера все сервисы, которые не [синие](../../contour/business_domain/business_offer.md) и не белые DBS-ы.

**3. Закрытие миграции неподдерживаемых офферов**

В Маркете есть процессы подключения офферов к бизнес-аккаунтам или смены `business_id` у них, что по сути переезд между бизнес-аккаунтами. Такой процесс иногда называют миграцией или бизнес-миграцией. Это многоступенчатая процедура, когда несколько подсистем Маркета должны дать свой ответ в формате "я сделаль", то есть сервис Х перевёз у себя этот оффер под нужный `business_id`. Наш сервис как раз является одним из участников цепочки. Однако прикол в том, что мы многие типы офферов вообще не обрабатываем. Соответственно, нам по ним решительно нечего мигрировать. Поэтому мы должны сразу при получении такого бесполезного для нас оффера дать отмашку, что мы будто бы закончили миграцию (если она вообще была по нему запущена). Именно это и происходит на данном шаге импорта, а за процесс миграции отвечает сервис [ServiceOfferMigrationService](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/datacamp/ServiceOfferMigrationService.java).

**4. Конвертация исходных CommonSsku в SilverCommonSsku**

Точка входа [DatacampOffersFiltrator](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/datacamp/SupplierSilverSskuTransformationService.java), метод `convertToSilver`.

Конвертация офферов в идеологически правильный формат, который пригоден для дальнейшей обработки и сохранения в БД.

- Всем офферам проставляется `source_type = SUPPLIER` и `source_id = DATACAMP`.
- Если во входном батче один и тот же оффер встречается больше одного раза, то он схлопывается в один. При схлопывании приоритет отдаётся офферу с самой свежей ЕОХ-версией.

На выходе получаем набор красивых `SilverCommonSsku`.

**5. Фильтрация DBS**

Точка входа — всё тот же `DatacampOffersFiltrator`, метод `applyColorFilter`.

Особый сценарий — это сервисная модель размещения DBS. МДМ поддерживает офферы с такими сервисами в ограниченном режиме. В МДМ завезено приблизительно несколько миллионов таких офферов, которые должны успешно обновляться. Также есть диапазон допустимых `business_id`, для которых DBS поддерживаются без дополнительных условий. С учётом вышеперечисленного процедура фильтрации имеет примерно такой вид:

1. Забираем из SKV настройку цветового фильтра. Если настройка в режиме `DbsImportMode.BLUE_AND_DBS`, то все офферы разрешены, конец фильтрации.
2. В противном случае разрешаем DBS-содержащий оффер, если его `business_id` попадает в разрешённый диапазон цветового фильтра, либо если в МДМ такой оффер уже и так существует (то есть, он уже заезжал в нас ранее и зарегистрирован в `mdm.ssku_existence`).
3. Если же оффер проверки не проходит, то мы удаляем из него все DBS-сервисы. При этом если у него вообще не осталось сервисов, то мы всё равно пропускаем его дальше по пайплайну, так как сервисы могут появиться позже от мержа с существующим серебром.

**6. Детекция изменений**

Точка входа `DatacampOffersImporterImpl`, метод `prepareForSave`.

Итак, мы имеем коллекцию красивых разрешённых для обработки серебряных SSKU. Теперь необходимо:

1. Прогрузить существующую версию этих SSKU из БД, если они есть
2. При помощи `DatacampOffersFiltrator` отбросить из входной коллекции те офферы, которые старше уже лежащих у нас в БД (защита от гонок)
3. Там же оставить только те SSKU, у которых есть фактически изменения в данных
4. С помощью `SupplierSilverSskuTransformationService` схлопнуть существующие у нас SSKU с пришедшими. Это необходимо из-за того, что ЕОХ зачастую присылает не полный набор сервисов, а только изменившиеся. Поэтому мы мёржим уже имеющиеся сервисы с новыми. Если после схлопывания итоговый оффер не имеет сервисов, то мы его отбрасываем.
5. С помощью `SupplierSilverSskuTransformationService` ищем те офферы, у которых все сервисы DBS. Для таких офферов меняем `source_type` целиком с `SUPPLIER` на менее приоритетный `DBS`. Это нужно потому, что такие чисто-DBS офферы обычно хуже по качеству, нежели SSKU с синими моделями размещения.
6. Берём ЕОХ-версию и распихиваем по всем частям каждого оффера.

**7. Сохранение**

Точка входа `DatacampOffersImporterImpl`, конец метода `importOffers`.

1. Сохраняем в нашу БД (в Yt-хранилище) офферы, героически прошедшие через предыдущие шаги.
2. В служебную табличку `mdm.ssku_existence` записываем маркеры существования сервисов для всех только что полученных сервисов для неудаленных офферов и удаляем маркеры для удаленных
3. Закрываем миграцию для всех сохранённых офферов тем же способом, что и для неподдерживаемых ранее.
4. Укладываем ключи офферов в очереди на обработку золота SSKU и на отправку в ERP.
5. Очищаем мусорное серебро из Yt-хранилища.

Мусорное серебро — это такие SSKU из нашей БД, у которых некорректный `source_id + source_type`, либо же оффер, сменивший свой `source_type` на `DBS` или обратно в `SUPPLIER`. То есть, мы вычищаем старый оффер с устаревшим или невалидным источником, и просто сызнова записываем правильный.

**8. Ошибки**

В случае возникновения исключения импорт останавливается и в читателе Логброкера ключики офферов складываются в специальную fail-очередь. Затем оттуда офферы переимпортируются независимым процессом при помощи синхронного сервиса [MdmDatacampService](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mbo-category/mbo-mdm-common/src/main/java/ru/yandex/market/mbo/mdm/common/datacamp/MdmDatacampServiceImpl.java).
