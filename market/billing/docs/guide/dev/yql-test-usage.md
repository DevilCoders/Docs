# Тестирование YQL-запросов

## Предварительная настройка

### 1. Добавьте переменную окружения ARCADIA_ROOT

Возможно, у вас уже прописана данная переменная в `~/.bash_profile`. Если так, то ничего делать не нужно.

**Способ 1:** добавьте переменную в `~/.bash_profile`.

Выполните скрипт, а затем перезапустите IDE:
```shell
echo 'export ARCADIA_ROOT=<абсолютный путь к корню Аркадии>' >> ~/.bash_profile
```

**Способ 2:** добавьте переменную в настройках запуска тестов в Idea.
1. Откройте шаблон запуска тестов: `Run -> Edit Configurations -> Edit configuration templates -> JUnit`.
2. Добавьте в поле Environment variables строчку `ARCADIA_ROOT=<абсолютный путь к корню Аркадии>` (если там уже есть переменные, используйте разделитель `;`).
3. Если у вас уже созданы конфигурации запуска отдельных тестов из шаблона, просто удалите их и запустите тесты заново.

### 2. Укажите свой токен для доступа к YQL

1. Получите свой токен в [интерфейсе YQL](https://yql.yandex-team.ru): `Settings -> Auth -> Show my token`.
2. Откройте шаблон запуска тестов: `Run -> Edit Configurations -> Edit configuration templates -> JUnit`
3. Добавьте в поле VM Options строчку `-Dmbi.robot.yql.token=<ваш токен> -Dyql.datasource.token=<ваш токен>`
4. Закомментируйте в functional-test.properties `yql.datasource.token`
5. Если у вас уже созданы конфигурации запуска отдельных тестов из шаблона, просто удалите их и запустите тесты заново.

Готово! Теперь вы можете запускать существующие тесты YQL локально!

## Написание теста

### 1. Используйте QueryService для формирования тестируемого YQL-запроса

1. `QueryService` является Spring-овым бином (синглтоном), поэтому его можно заавтовайрить.
2. Напишите или перенесите yql-запрос в файл шаблона для движка Freemarker в директорию
[queries](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/resources/queries) в ресурсах.
3. Параметры запроса, принимаемые извне, объявите в виде параметров шаблона (пример: `${supply_types}`).
4. Адреса таблиц для select-запросов объявите в виде вызова функции `tbl` с адресом реальной таблицы в качестве параметра
(пример: `select from ${tbl("${table_supplies_import_latest}")}`).
5. Адреса таблиц для insert-запросов объявите в виде вызова функции `tbl_wo_inline` с адресом реальной таблицы в качестве параметра
(пример: `insert into ${tbl_wo_inline("${report_table}")}`).
6. Для формирования запроса в рантайме, вызовите метод `QueryService.getQuery()`.

Пример шаблона запроса (Freemarker):
```sql
select
   sr.id as id,
   sr.type_name as type_name,
   sr.status_name as status_name,
   sr.external_operation_type as external_operation_type,
   sr.created_at as created_at,
   sr.updated_at as updated_at,
   sr.service_request_id as service_request_id,
   sr.actual_pallet_amount as actual_pallet_amount,
   sr.actual_box_amount as actual_box_amount,
   sr.x_doc_service_id as x_doc_service_id,
   sr.service_id as service_id
from ${tbl("${table_supplies_import_latest}")} as sr
where sr.status_name in (${supply_statuses})
    and (sr.type_name in (${supply_types})
      or (type = 3 and external_operation_type = 9 and to_stock_type = 4))
```

Пример кода формирования запроса из вышеуказанного шаблона:
```java
private String createSuppliesQuery() {
    Map<String, Object> params = Map.of(
            "table_supplies_import_latest", supplyLatestTable,
            "supply_types", collectionToInStatement(SUPPLY_IMPORT_TYPES),
            "supply_statuses", collectionToInStatement(SUPPLY_IMPORT_STATUSES)
    );
    return queryService.getQuery("fulfillment_supply.import.yql", params);
}
```

Готово! Теперь запрос формируется с помощью `QueryService`, что позволит в тестах подменять адреса реальных таблиц на тестовые.

### 2. Создайте файлы схем для таблиц YT

Для каждой таблицы, к которой обращается YQL-запрос, выполните скрипт
[download_schema.sh](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/test/bin/download_schema.sh):
```shell
bash download_schema.sh //home/market/production/mstat/dictionaries/fulfillment_shop_request/1d/latest
```

Отлично! Теперь в локальной директории
[src/test/resources/yt/schemas](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/test/resources/yt/schemas/)
появились все необходимые схемы для создания тестовых таблиц, которые будут подменять реальные.

### 3. Задайте исходные данные, которыми будут наполнены таблицы

Это делается с помощью csv-файлов такого формата:
```
//home/market/production/mstat/dictionaries/fulfillment_shop_request/1d/latest
id,type_name,status_name,created_at,updated_at
1,"Поставка","Товары приняты","2021-05-18 18:29:41.351734","2021-05-18 18:29:41.351734"
````

Расположение: непосредственно в папке с тестом.<br/>
Название: `<Имя тестового класса>.<имя тестового метода>.yt.csv`.

{% note info %}

В одном файле можно указывать несколько таблиц, разделённых пустой строкой.

{% endnote %}


{% note info %}

Можно указывать только обязательные поля (которые объявлены в схеме с параметром `required=true`), остальные в этом случае заполнятся `null`-ами.

{% endnote %}

Превосходно! До работающего теста осталось совсем немного! Теперь библиотека сможет не только создать таблицы, но и наполнить их данными.

### 4. Создайте файлик для кэширования ответа YQL

Теперь нам нужен файл, в который библиотека сохранит ответ от настоящего YQL, чтобы при последующих запусках не обращаться
к YQL, если исходные данные и запрос не изменились.

Расположение: непосредственно в папке с тестом.<br/>
Название: `<Имя тестового класса>.<имя тестового метода>.yt.mock`.<br/>
Содержимое: `[]`.

### 5. Напишите тест и укажите аннотацию @YqlTest

Пример:
```java
class FulfillmentSupplyYtDaoSuppliesTest extends FunctionalTest {

    @Test
    @YqlTest(
            // корневая директория схем, её не меняем
            schemasDir = "/yt/schemas",
            // здесь перечислите все таблицы, используемые в тестируемом YQL-запросе
            // (для них должны быть извлечены и сохранены на диск файлы схем (шаг 2)
            schemas = {
                    "//home/market/production/mstat/dictionaries/fulfillment_shop_request/1d/latest"
            },
            // csv-файл с данными для указанных выше таблиц
            csv = "FulfillmentSupplyYtDaoSuppliesTest.selectsOnlyRequiredStatuses.yql.csv",
            // файл с кэшем ответа от YT
            yqlMock = "FulfillmentSupplyYtDaoSuppliesTest.selectsOnlyRequiredStatuses.yql.mock"
    )
    public void yourTest() {
        // 1. вызовите код, который обращается к YQL
        // 2. проверьте результат его работы (например, с помощью библиотеки Assertions или аннотации @DbUnitDataSet)
        // 3. если код выполняет пишущий yql-запрос и хочется проверить результат его работы в YT, то читайте следующий пункт
    }
}
```

Шикарно! Теперь при запуске данного теста библиотека перехватит запрос к YQL через локальный прокси, создаст тестовые таблички, наполнит их данными,
а YQL-запрос изменит так, что он будет обращаться к тестовым табличкам вместо продакшеновых. Ответ от YQL библиотека закэширует в указанном mock-файле.

### 6. (Для тестирования пишущих YQL-запросов) Укажите ожидаемое содержимое таблиц после выполнения теста

Создайте csv-файл с ожидаемыми данными и укажите его в аннотации `@YqlTest.expectedCsv`.

Пример csv:
```
//home/market/production/mbi/reports/stocks_on_warehouses/full_latest
warehouse_id,warehouse_name,supplier_id,shop_sku,actual_date,available,defect,utilization
147,"Ростов-на-Дону",101,"101-1","2021-12-21",7,1,0
```

### 7. Закоммитьте файлы в репозиторий

Закоммитьте в репозиторий:
- схемы таблиц YT;
- csv-файлы с исходными данными;
- mock-файлы с ответом от YQL.

## Примеры

- Тест с проверкой результатов с помощью кода: [FulfillmentSupplyYtDaoSuppliesTest](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/test/java/ru/yandex/market/billing/fulfillment/supplies/dao/FulfillmentSupplyYtDaoSuppliesTest.java)
- Тест с проверкой результатов с помощью `@DbUnitDataSet`: [DailyImportSupplyServiceTest](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/test/java/ru/yandex/market/billing/fulfillment/supplies/DailyImportSupplyServiceTest.java) (см. метод `test_batchInsertSupplies()`)
