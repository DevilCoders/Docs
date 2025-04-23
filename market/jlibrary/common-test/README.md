# common-test
Набор утилитных классов для поддержки модульного тестирования.
- [Сборка и тестирование](#Сборка-и-тестирование)
- [Релизы](#Релизы-в-ЦУМе)
- [Что умеет](#Что-умеет)
  - [Интеграция с БД](#Интеграция-с-БД)
    - [Настройка junit для работы со Spring](#Настройка-junit-для-работы-со-spring)
    - [Инициализация БД](#Инициализация-БД)
    - [Наполнение и проверка БД](#Наполнение-и-проверка-БД)
      - [Аннотация `@DbUnitDataSet`](#Аннотация-dbunitdataset)
      - [Форматы для наборов данных](#Форматы-для-наборов-данных)
      - [Что можно указывать в качестве значения](#Что-можно-указывать-в-качестве-значения)
      - [Комментарии](#Комментарии)
    - [Переписывание запросов](#Переписывание-запросов)
  - [Интеграция через `RestTemplate`](#Интеграция-через-resttemplate)
    - [Как включить](#Как-включить)
      - [`MyTest.java`](#mytestjava)
      - [`myClient.json`](#myclientjson)
    - [Как работает](#Как-работает)
  - [Проверка форматов выдачи](#Проверка-форматов-выдачи)
    
## Сборка и тестирование
[ya.make](https://wiki.yandex-team.ru/yatool/make/)    
    
## Релизы в ЦУМе
[pipeline](https://tsum.yandex-team.ru/pipe/projects/jlibrary/pipelines/common-svn), 
[dashboard](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/common-svn)

## Что умеет

1. Работает внутри Spring
2. Тестирование работы с БД. Сюда входит инициализация, наполнение и сравнение состояния с эталоном.
3. Описание наборов данных в удобном виде (`.csv`, содержащий сразу несколько таблиц).
4. Очистка всех таблиц и сброс sequence перед каждым тестом.
5. Преобразование SQL-запросов из диалекта боевой СУБД в тестовую. Есть несколько правил для перевода из Oracle в H2.
6. "Заглушки" для клиентов, использующих `RestTemplate`.
 
### Интеграция с БД

#### Подготовка схемы

Возможны 3 варианта:

1. Схема БД указывается, например, в liquibase в диалекте, который одинаково хорошо воспринимается целевой СУБД и 
тестовой (например, H2). Тогда можно перед тестом применять liquibase.
2. Схема БД для тестов ведётся отдельно. 
3. Можно использовать таск `dumpSchema` из gradle плагина `mbuild-dbtools`.

Пример конфигурации таска можно посмотреть в [репозитории mbi](https://github.yandex-team.ru/market-java/mbi/blob/master/mbi-db/build.gradle#L172).

Пример запуска:
```bash
./gradlew dumpSchema -PschemaTables=TABLE1,TABLE2 -Pschemas=SCHEMA -Pdialect=h2
```

Таск читает описания таблиц из целевой СУБД (сейчас поддерживается Oracle и есть какие-то зачатки для PostgreSQL) и
складывает их диалекте тестовой СУБД (H2 или HSQLDB).

Что умеет переводить:

1. Таблицы/столбцы всех основных типов, `not null` поля.
2. `default my_seq.nextval` или `identity` переводятся в явное создание sequence и аналогичное объявление значения
по-умолчанию.
3. Индексы - уникальные и обычные.
4. Первичные ключи, в том числе составные.
5. Внешние ключи, в том числе составные.

#### Настройка junit для работы со Spring

На тестовый класс нужно навесить несколько аннотаций:

```java
@RunWith(SpringJUnit4ClassRunner.class)
@TestExecutionListeners({
        DirtiesContextTestExecutionListener.class,
        DependencyInjectionTestExecutionListener.class,
        DbUnitTestExecutionListener.class
})
@ContextConfiguration(classes = MyConfig.class)
public class MyTest {
}
```

1. `@RunWith` - включаем Spring для теста.
2. `@TestExecutionListeners` - первые два слушателя стандартные. Третий - будет заниматься наполнением и сравнение БД.
Если используется Spring 4.2+, то можно стандартные не указывать, заменив их на `(mergeMode = MERGE_WITH_DEFAULTS)`.
3. `@ContextConfiguration` - указываем класс-конфигурацию для спринг-контекста. 

Чтобы не перечислять каждый раз `@TestExecutionListeners`, можно унаследовать тестовый класс от `DbUnitTest`. 

#### Инициализация БД

В целом - можно инициализировать любым удобнымм способом. Однако есть удобный базовый конфиг (`DbUnitTestConfig), 
создающий и инициализирующий БД, регистрирующий большинство необходимых бинов в спринге:

1. `dataSource`
2. `jdbcTemplate`
3. `namedParameterJdbcTemplate`
4. `transactionTemplate` 
5. `txManager`

```java
@Configuration
public class MyConfig extends DbUnitTestConfig {
        @Override
        public EmbeddedDatabaseFactoryBean dataSourceFactory() {
            return createDataSourceFactory(
                    EmbeddedDatabaseType.H2
                    /*, varargs со списком ресурсов с DDL */
            );
        }
}
```

#### Наполнение и проверка БД

##### Аннотация @DbUnitDataSet

На тестовый класс или метод можно навесить аннотацию `@DbUnitDataSet`. В этом случае перед запуском теста будут очищены
все таблицы в БД в `dataSource` (в имя бина в спринге), и сброшены в 1 все sequence (явные и identity). После этого 
на БД наливаются наборы данных из атрибута `before` аннотаций на классе и на методе. Путь до файлов указывается 
относительно тест-класса. То есть по умолчанию набор данных берётся из того же пакета.

После выполнения теста состояние БД сравнивается с наборами данных в файлах в атрибутах `after()`. Сравнение
выполняется:
 
1. Только для таблиц, присутствующих в after.
2. Сравниваются только указанные в after столбцы.
3. Сравнение производится построчно после сортировки по возврастанию по всем указанным столбцам.

То есть не нужно подбирать автогенерённые id/timestamp и порядок строк.  

Из этого правила могут быть исключения. Чтобы выбрать неощичаемые таблицы, можно указать атрибут `nonTruncatedTables`.
Это множественный атрибут, полное значение для которого будет собрано по всем классам в иерархии и всем интерфейсам,
которые реализует текущий тест-класс. Например:

```java
@DbUnitDataSet(nonTruncatedTables = "tab1")
interface Ignore1 {}

@DbUnitDataSet(nonTruncatedTables = "tab2")
interface Ignore2 extends Ignore1 {}

@DbUnitDataSet(nonTruncatedTables = "tab3")
class Ignore3 {}

@DbUnitDataSet(nonTruncatedTables = "tab4")
class MyTest extends Ignore3 implements Ignore2 {
    @Test
    @DbUnitDataSet(nonTruncatedTables = "tab5")
    @DbUnitDataSet(nonTruncatedTables = "tab6")
    public void doTest() {
    }
}
```

В этом случае будут очищены все таблицы, кроме `tab1...tab6`. 

Если имя бина `DataSource` отличается от `dataSource`, его можно указать в атрибуте `DbUnitDataSet.dataSource()`.
Эта фича работает пока с точным указанием в каждом `DbUnitDataSet`. TODO: сделать вывод из ближайшего родителя. 

##### Форматы для наборов данных

Формат описания можно указать в атрибуте `@DbUnitDataSet.type`. По умолчанию - `SINGLE_CSV`.

1. [XML](http://dbunit.sourceforge.net/apidocs/org/dbunit/dataset/xml/XmlDataSet.html)
2. [FLATXML](http://dbunit.sourceforge.net/apidocs/org/dbunit/dataset/xml/FlatXmlDataSet.html)
3. [CSV](http://dbunit.sourceforge.net/apidocs/org/dbunit/dataset/csv/CsvDataSet.html)
4. `SINGLE_CSV` - кастомный формат, позволяющий описать несколько таблиц в одном CSV файле. Выглядит это примерно так:

```csv
SCHEMA.TABLE_1
COL1,COL2
1,"VALUE 1"
2,"VALUE 2"

SCHEMA.TABLE_2
COL1,COL2
1,"VALUE 1"
2,"VALUE 2"
```

1. Полное имя таблицы `SCHEMA.TABLE_1`.
2. Список столбцов для заполнения/сравнения. Если столбец не указан, то при наполнении будет использовано 
значение по умолчанию, а при сравнении - столбец не будет учтён.
3. Значения столбцов.
4. Пустая строка, отделяющая таблицы друг от друга.

##### Что можно указывать в качестве значения

1. `null` - если нужно NULL в поле.
2. Обычный литерал числа/строки. Если в строке есть запятые, то значение нужно брать в двойные кавычки. Если 
двойные кавычки, то 2 символа двойных кавычек.
3. Литерал даты в формате `YYYY-MM-DD`.
4. Вычисляемые значения (только для SINGLE_CSV). Выражение можно завернуть в `${}` и что-нибудь вычислить. Например,
есть функции для вычисления дат:

1. `sysdate(days, [hours], [minutes], [seconds])` - возвращает текущую дату смещённую на указанное количество дней, 
минут, секунд. Например `${sysdate(-1)}` вернёт _вчера в то же время_, а `${sysdate(0, -1)}` вернёт _час назад_.

##### Комментарии

В `SINGLE_CSV` файле можно писать комментарии. Такие строки должны начинаться с символа `#` и будут проигнорированы при
применении набора.
 
#### Переписывание запросов

Если существуют различия в диалекте DML-запросов между целевой и тестовой СУБД, то можно пользоваться классом 
`InstrumentedDataSource` для подмены запросов. В частности, это может потребоваться для передачи массива значений в 
качестве параметра в запрос (т.к. в Oracle это делается очень неочевидным способом).

Пример можно посмотреть в [`DbUnitTestConfig.java`](https://github.yandex-team.ru/market-java/common-test/blob/master/src/main/java/ru/yandex/market/common/test/spring/DbUnitTestConfig.java).

Пример теста [`SampleTest.java`](https://github.yandex-team.ru/market-java/common-test/blob/master/src/test/java/ru/yandex/market/common/test/db/SampleTest.java).

Полный список реализованных модификаций для Oracle->H2 можно посмотреть [`H2SqlTransformer.java`](https://github.yandex-team.ru/market-java/common-test/blob/master/src/main/java/ru/yandex/market/common/test/jdbc/H2SqlTransformer.java)

### Интеграция через RestTemplate

#### Как включить

##### MyTest.java
```java
public class MyTest {
    RestTemplate restTemplate;
    @Before
    public void init() {
        restTemplate.setRequestFactory(new MockClientHttpRequestFactory(
                new ClassPathResource("myClient.json")
        ));
    }
}
```

##### myClient.json

```json
{
    "/path?param1=0": { // более специфичный запрос
        "result": {
            "field": "value1"
        }
    },
    "/path": { // менее специфичный запрос
        "result": {
            "field": "value2"
        }
    },
    "/myObj/*": { // маска в path
        "result": {
            "field": "value"        
        }
    }
}
```

#### Как работает

Файл `myClient.json` содержит соответствия `url - ответ`. В url можно указывать как путь от корня, так и параметры.
При выполнении запроса выполняется поиск нужного ответа по порядку сверху вниз. Под сравнение попадают путь и 
все указанные в `myClient.json` параметры. Поэтому располагать нужно сначала более специфичные запросы.

Например, на запрос `/path?param1=0` будет выдан первый ответ, а на запрос `/path?param1=1` - второй. 

### Проверка форматов выдачи

```java
public class MyTest {
    @Test
    public void test() {
        new SerializationChecker(
                o -> "{}",
                json -> new Object(),
                o -> "<obj/>",
                xml -> new Object() 
        ).test(
                new Object(), // оригинал
                new Object(), // объект, после сериализации и обратной десериализации из оригинала
                "{}",         // ожидаемый json
                "<obj/>"      // ожидаемый xml
        );
    }
}
```
