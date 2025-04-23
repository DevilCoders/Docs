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
4. Если у вас уже созданы конфигурации запуска отдельных тестов из шаблона, просто удалите их и запустите тесты заново.
5. Если пункты выше не помогли, добавьте свой токен в поле yql.datasource.token в [properties](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/report-generator/src/test/resources/ru/yandex/market/rg/config/functional-yql-test.properties)

Готово! Теперь вы можете запускать существующие тесты YQL локально!

## Написание теста

### 1. Используйте QueryService для формирования тестируемого YQL-запроса

1. `QueryService` является Spring-овым бином (синглтоном), поэтому его можно заавтовайрить.
2. Напишите или перенесите yql-запрос в файл шаблона для движка Freemarker в директорию
[queries](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/report-generator/src/main/resources/queries) в ресурсах.
3. Параметры запроса, принимаемые извне, объявите в виде параметров шаблона (пример: `${table_payout_latest}`).
4. Адреса таблиц для select-запросов объявите в виде вызова функции `tbl` с адресом реальной таблицы в качестве параметра
(пример: `select from ${tbl("${table_payout_latest}")}`).
5. Адреса таблиц для insert-запросов объявите в виде вызова функции `tbl_wo_inline` с адресом реальной таблицы в качестве параметра
(пример: `insert into ${tbl_wo_inline("${report_table}")}`).
6. Для формирования запроса в рантайме, вызовите метод `QueryService.getQuery()`.

Пример шаблона запроса (Freemarker):
```sql
select
    p.payout_id as id
from ${tbl("${table_payout_latest}")} as p
```

Пример кода формирования запроса из вышеуказанного шаблона:
```java
    private String selectPayoutsQuery() {
    Map<String, Object> params = Map.of(
        "table_payout_latest", payoutTablePath
    );
    return queryService.getQuery("bank_order_info.yql", params);
    }
```

Готово! Теперь запрос формируется с помощью `QueryService`, что позволит в тестах подменять адреса реальных таблиц на тестовые.

### 2. Создайте файлы схем для таблиц YT

Для каждой таблицы, к которой обращается YQL-запрос, выполните скрипт
[download_schema.sh](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/report-generator/src/test/bin/download_schema.sh):
```shell
bash download_schema.sh //home/market/production/billing/dictionaries/payout/latest
```

Отлично! Теперь в локальной директории
[src/test/resources/yt/schemas](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/report-generator/src/test/resources/yt/schemas/)
появились все необходимые схемы для создания тестовых таблиц, которые будут подменять реальные.

### 3. Задайте исходные данные, которыми будут наполнены таблицы

Это делается с помощью csv-файлов такого формата:
```
//home/market/production/billing/dictionaries/payout/latest
payout_id,entity_id,checkouter_id,transaction_type,product,paysys_type_cc,order_id,partner_id,trantime,amount,payout_group_id,entity_type,paysys_partner_id,accrual_id,org_id,date
33169833,160986229,119058003,"payment","partner_payment","acc_sberbank",97452406,1051563,"2022-03-21 15:00:25.521",220000,3997097,"item",null,null,64554,"2022-04-05"
````

Расположение: непосредственно в папке с тестом.<br/>
Название: `<Имя тестового класса>.<имя тестового метода>.yt.csv`.

В одном файле можно указывать несколько таблиц, разделённых пустой строкой.

Можно указывать только обязательные поля (которые объявлены в схеме с параметром `required=true`), остальные в этом случае заполнятся `null`-ами.

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
                "//home/market/production/billing/dictionaries/payout/latest"
            },
            // csv-файл с данными для указанных выше таблиц
            csv = "BankOrderInfoYtDaoTest.selectsPayouts.yql.csv",
            // файл с кэшем ответа от YT
            yqlMock = "BankOrderInfoYtDaoTest.selectsPayouts.yql.mock"
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

- Тест [BankOrderInfoYtDaoTest](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/report-generator/src/test/java/ru/yandex/market/core/order/BankOrderInfoYtDaoTest.java)
- Тест с проверкой результатов с помощью кода: [FulfillmentSupplyYtDaoSuppliesTest](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/test/java/ru/yandex/market/billing/fulfillment/supplies/dao/FulfillmentSupplyYtDaoSuppliesTest.java)
- Тест с проверкой результатов с помощью `@DbUnitDataSet`: [DailyImportSupplyServiceTest](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/test/java/ru/yandex/market/billing/fulfillment/supplies/DailyImportSupplyServiceTest.java) (см. метод `test_batchInsertSupplies()`)
