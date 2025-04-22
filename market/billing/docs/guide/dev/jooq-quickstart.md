# Jooq: быстрый старт

На данный момент Jooq настроен для обращения к Postgres Биллинга и доступен для использования в проекте `market-billing-tms`.

## Входная точка: DSLContext

Работа с Jooq производится с помощью бина `DSLContext`. Он является спринговым синглтоном, поэтому его можно заавтовайрить:

```java
@Autowired
private DSLContext dslContext;
```

## DSL для SQL-запросов

В построении запросов на Jooq вам будет помогать автоподстановка IDE,
а так как синтаксис Jooq имитирует уже знакомый SQL, вы легко узнаете предлагаемые конструкции.
Всё что нужно знать - это входные точки Jooq DSL.

### org.jooq.DSLContext: входная точка

Когда мы пишем в теле метода `dslContext.`, то IDE сразу предлагает массу знакомых вариантов,
как может начинаться запрос: `select`, `insertInto`, `update`... Выбираем подходящий.

В запросе нам потребуется указать таблицы и поля, с которыми мы хотим работать. Эти сущности генерируются на основе liquibase-схемы.
Сгенерированные таблички лежат в виде статических полей в классах `Tables`, по одному на каждую схему. А внутри табличек лежат поля.

Вводим `Tables` и IDE предлагает варианты: `ru.yandex.market.billing.dbschema.shops_web.Tables` и
`ru.yandex.market.billing.dbschema.market_billing.Tables`, выбираем подходящий и пишем нужную табличку,
например `Tables.ACCRUAL`.

Пример:
```java

import static ru.yandex.market.billing.dbschema.shops_web.Tables.REGIONS;

...

    // выбираем названия регионов из таблицы shops_web.regions с limit + offset
    private List<String> getRegionNames(int limit, int offset) {
        return dslContext
                .select(REGIONS.NAME)
                .from(REGIONS)
                .orderBy(REGIONS.ID)
                .limit(limit)
                .offset(offset)
                .fetch(Record1::value1);
    }
```

Можно получить мапу id -> name:
```java
    private Map<Long, String> getRegionNames() {
        return dslContext
                .select(REGIONS.ID, REGIONS.NAME)
                .from(REGIONS)
                .fetchMap(Record2::value1, Record2::value2);
    }
```

{% note info %}

Используйте `import static` для таблиц из класса `Tables`, это делает код чище и больше похожим на SQL: `dslContext.select(ACCRUAL.AMOUNT)`.

{% endnote %}

{% note info %}

Если при вводе `.select(` Idea начинает тормозить, закройте подсказку со списком перегруженных методов нажатием ESC.

{% endnote %}

### Секция "WHERE"

Основной входной точкой для формирования условий (`org.jooq.Condition`) для секции `where` являются сгенерированные поля.
Вводим поле `REGIONS.ID.` и IDE предлагает варианты условий: `eq`, `in`, `gt` (greater than), `ge` (greater or equal) и другие.

Пример:
```java
    private List<String> getRegionNames(List<Long> ids) {
        return dslContext
                .select(REGIONS.NAME)
                .from(REGIONS)
                .where(REGIONS.ID.in(ids))
                .fetch(Record1::value1);
    }
```

Пример составного условия:
```java
    private Map<Long, String> getRegionNames(List<Long> ids) {
        return dslContext
                .select(REGIONS.ID, REGIONS.NAME)
                .from(REGIONS)
                .where(REGIONS.ID.in(ids).and(REGIONS.NAME.isNotNull()))
                .fetchMap(Record2::value1, Record2::value2);
    }
```

### Секция "JOIN"

Условие в секции join формируется на основе полей, как и в секции WHERE.<br/>
Пример:
```java
    public List<Long> getGlobalAccrualIdsForPayoutGeneration() {
    return dslContext
            .select(ACCRUAL.ID)
            .from(ACCRUAL)
            .join(ORDER_PAYOUT_TRANTIME)
            .on(ORDER_PAYOUT_TRANTIME.PARTNER_ID.eq(ACCRUAL.PARTNER_ID)
                    .and(ORDER_PAYOUT_TRANTIME.ORDER_ID.eq(ACCRUAL.ORDER_ID)))
            .where(ACCRUAL.PAYOUT_STATUS.eq(PayoutStatus.NEW.getId()))
            .and(ACCRUAL.ORG_ID.in(OperatingUnit.GLOBAL_ORG_IDS))
            .fetch(Record1::value1);
    }
```

### org.jooq.DSL: дополнительная входная точка

В классе `org.jooq.DSL` есть дополнительные штучки вроде `DSL.count()` для формирования запроса `select count(*)`.
Так же есть класс `org.jooq.util.postgres.PostgresDSL`, в котором теоретически можно найти что-то специфичное для Postgres.

Пример:
```java
    public Integer count() {
        return dslContext
                .select(DSL.count())
                .from(REGIONS)
                .fetchOne()
                .value1();
    }
```

## Маппинг полей при чтении и записи

### JooqMapper

JooqMapper предназначен для маппинга полей DTO на поля сгенерированных классов Jooq.
Он предоставляет декларативный DSL для описания маппинга:
- какое поле БД какому полю объекта соответствует (возможнен маппинг нескольких полей БД на одно поле объекта и наоборот)
- как сконвертировать поле БД в поле объекта и наоборот

Описанный в одном месте маппинг затем используется для чтения и записи.

Класс `JooqMapper` является надстройкой над двумя сущностями: `JooqReader` и `JooqWriter`, которые могут использоваться независимо.

JooqMapper требует объявленных `ModelProperty` в классе DTO. `ModelProperty`, в свою очередь,
довольно плохо совмещаются с иммутабельными объектами. Однако, во многих случаях очевидные преимущества связки Jooq + JooqMapper
для написания запросов в БД превышают ту защиту от рисков, которую предоставляют иммутабельные объекты.

Пример:
```java
public class Region implements Model {

    public static ModelProperty<Region, Long> ID =
            ModelProperty.create(Region.class, "id", Region::getId, Region::withId);

    public static ModelProperty<Region, String> NAME =
            ModelProperty.create(Region.class, "name", Region::getName, Region::withName);

    public static ModelProperty<Region, RegionType> REGION_TYPE =
            ModelProperty.create(Region.class, "regionType", Region::getRegionType, Region::withRegionType);

    private Long id;
    private String name;
    private RegionType regionType;

    public Long getId() {
        return id;
    }

    public Region withId(Long id) {
        this.id = id;
        return this;
    }

    public String getName() {
        return name;
    }

    public Region withName(String name) {
        this.name = name;
        return this;
    }

    public RegionType getRegionType() {
        return regionType;
    }

    public Region withRegionType(RegionType regionType) {
        this.regionType = regionType;
        return this;
    }
}


import static ru.yandex.direct.jooqmapper.ReaderWriterBuilders.convertibleProperty;
import static ru.yandex.direct.jooqmapper.ReaderWriterBuilders.property;
import static ru.yandex.market.billing.dbschema.shops_web.Tables.REGIONS;

public class RegionsDao {
    private final DSLContext dslContext;
    private final JooqMapperWithSupplier<Region> mapper;

    public RegionsDao(DSLContext dslContext) {
        this.dslContext = dslContext;
        this.mapper = createMapper();
    }

    public List<Region> get(Collection<Long> ids) {
        return dslContext
            .select(mapper.getFieldsToRead())
            .from(REGIONS)
            .where(REGIONS.ID.in(ids))
            .fetch(mapper::fromDb);
    }

    public void add(List<Region> regions) {
        InsertHelper.saveModelObjectsToDbTable(dslContext, REGIONS, mapper, regions);
    }

    private JooqMapperWithSupplier<Region> createMapper() {
        return JooqMapperWithSupplierBuilder.builder(Region::new)
            .map(property(ID, REGIONS.ID))
            .map(property(NAME, REGIONS.NAME))
            .map(convertibleProperty(REGION_TYPE, REGIONS.TYPE,
                this::regionTypeFromCode, this::regionTypeToCode))
            .build();
    }

    private RegionType regionTypeFromCode(Short regionTypeShort) {
        return RegionType.getRegionTypeByCode(regionTypeShort, true);
    }

    private Short regionTypeToCode(RegionType regionType) {
        return Integer.valueOf(regionType.getCode()).shortValue();
    }
}
```

## Хэлперы для пишущих запросов

### InsertHelper - хэлпер для формирования запросов "INSERT"

Использование исходного Jooq DSL для вставки списка объектов порождает довольно громоздкий код.
Чтобы избежать этих сложностей, можно использовать связку инструментов JooqMapper + InsertHelper.
Это позволяет скрыть детали работы с оригинальным Jooq DSL и сделать написание таких запросов очень простым и чистым.

Простейший пример:
```java
    public void add(List<Region> regions) {
        InsertHelper.saveModelObjectsToDbTable(dslContext, REGIONS, regionMapper, regions);
    }
```

Пример прямой установки поля в базе без использования JooqMapper:
```java
    public void add(List<Region> regions) {
        InsertHelper<RegionsRecord> insertHelper = new InsertHelper<>(dslContext, REGIONS);
        regions.forEach(region -> {
            insertHelper
                    .add(mapper, region)
                    .set(REGIONS.SOME_FIELD, 0L)
                    .newRecord(); // очень важно после каждой итерации вызывать этот метод
        });
        insertHelper.executeIfRecordsAdded();
    }
```

Использование InsertHelper с несколькими мапперами:
```java
    public void add(DSLContext dslContext, List<Region> regions) {
        InsertHelper<RegionsRecord> insertHelper = new InsertHelper<>(dslContext, REGIONS);
        regions.forEach(region -> {
            insertHelper.add(mapper, region);
            insertHelper.add(additionalMapper, region.getAdditionalInfo());
            insertHelper.newRecord(); // очень важно после каждой итерации вызывать этот метод
        });
        insertHelper.executeIfRecordsAdded();
    }
```

### Использование InsertHelper для запросов "INSERT ... ON CONFLICT"

```java
import static ru.yandex.market.billing.util.JooqPostgresUtils.excluded;

...

    public void mergeShopSkuInfos(List<ShopSkuInfo> shopSkuInfos) {
        if (shopSkuInfos.isEmpty()) {
            return;
        }

        InsertHelper<ShopSkuInfoRecord> insertHelper = new InsertHelper<>(dslContext, SHOP_SKU_INFO);
        insertHelper.addAll(shopSkuInfoMapper, shopSkuInfos);
        insertHelper.onDuplicateKeyUpdate()
                .set(SHOP_SKU_INFO.LENGTH, excluded(SHOP_SKU_INFO.LENGTH))
                .set(SHOP_SKU_INFO.WIDTH, excluded(SHOP_SKU_INFO.WIDTH))
                .set(SHOP_SKU_INFO.HEIGHT, excluded(SHOP_SKU_INFO.HEIGHT))
                .set(SHOP_SKU_INFO.WEIGHT, excluded(SHOP_SKU_INFO.WEIGHT));
        insertHelper.execute();
    }
```

## Генерация схемы Jooq

Jooq позволяет генерировать описания таблиц и их колонок на основе схемы базы данных, что в свою очередь даёт возможность
использовать всю мощь статической типизации и автоподстановки в IDE при использовании Jooq DSL.

В каком случае вам потребуется перегенерация схемы Jooq:
- вы изменяете схему БД, внося изменения в датасеты liquibase, и хотите, чтобы эти изменения попали в схему Jooq
- вы видите, что схема Jooq отличается от схемы БД, так как до вас кто-то внес изменения в схему БД и не перегенерировал схему Jooq

Всё что вам нужно сделать, это выполнить скрипт
`market/billing/libs-internal/jooq-db-schema-gen/bin/dbschemagen.sh` из любой директории.

{% note info %}

Не забудьте закоммитить изменения в сгенерированных классах.

{% endnote %}

### Переопределение типов полей при генерации схемы Jooq

Если тип поля в БД не соответствует тому, что в нём фактически хранится,
вы можете сгенерировать класс Jooq с другим, но совместимым типом.

Например, в поле фактически хранятся целочисленные значения, но тип почему-то объявлен как `numeric`
и в сгенерированном классе Jooq появляется `BigDecimal`.

Для этого добавьте переопределение поля в один из классов для соответствующей схемы:
- [MarketBillingForcedTypes](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/libs-internal/jooq-db-schema-gen/src/main/java/ru/yandex/market/billing/jooqdbschemagen/settings/MarketBillingForcedTypes.java)
- [ShopsWebForcedTypes](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/libs-internal/jooq-db-schema-gen/src/main/java/ru/yandex/market/billing/jooqdbschemagen/settings/ShopsWebForcedTypes.java)
