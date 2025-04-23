## Кубик Нирваны для реализации Prepared Statement запросов в YQL

### Описание
Этот кубик реализует безопасное подставление параметров в запросы YQL через именованные выражения [DECLARE](https://yql.yandex-team.ru/docs/yt/syntax/declare). 
Такие выражения парметризируют запросы и передают в базу данных параметры отдельно от самого запроса, используя транзакционные функции базы данных. Иначе это называют [Prepared Statement](https://wiki.yandex-team.ru/security/for/web-developers/#sql-injection).

Prepared Statement запросы полезны не только в плане безопасности, они создают меньшую нагрузку на базу данных, тк не требую перекомпиляции уже готового запроса, если вам требуется посылать много одинаковых запросов с разными параметрами.

Кубик принимает запрос, данные и исходя из типа данных в Declare пытается привести его к нужному типу, чтобы отправить его в YQL. Это нужно, так как YQL имеет свои типы, которые отличаются от Json Schema, и некоторые типы данных по-разному живут в json и YQL, что требует их приведения к общему виду. 


### Схема работы кубика
Кубик принимает на вход две сущности:
- Параметры в формате json на вход. Прочитать про формат поставки данных внутри json можно в разделе "Формат передачи данных в json".
- Query свойство кубика, в которое должен быть описан YQL запрос с использованием Declare. Пример использования можно увидеть в разделе "Примеры использования".

Пример работы можно увидеть в разделе "Примеры использования".

**Шаг 1**

Под капотом кубика используется [лексер](https://a.yandex-team.ru/arc_vcs/ydb/library/yql/parser?) YQL, который разбирает поданный запрос в query и выделяет из него DECLARE в принятом [синтаксисе](https://yql.yandex-team.ru/docs/yt/types/).
_Вам следует использовать принятый синтаксис, иначе лексер не сможет разобрать ваше выражение. Например, лексер не поймет int или int32 и вызовет исключение._
_Поскольку пока мы поддерживаем только примитивные и опциональные типы данных, синтакси вы можете увидеть [тут](https://yql.yandex-team.ru/docs/yt/types/primitive)._
_Сам Declare поддерживает только сериализуемые типы данных, будьте внимательны._

**Шаг 2**

Поданные данный в json формате сериализуются в python объект. 
_В этом месте не забывайте следовать общепринятой json схемы данных и оговоренных форматов передачи данных в зависимости от того, какой тип данных будет использоваться в Declare._
Оговоренную схему передачи данных в json и типу Declare можно увидеть в разделе "Формат передачи данных в json".


**Шаг 3**

По разобранному запросу выделяются переменные, содержимое которых ищется в сериализованном json. Содержимое ищется в словаре по ключу, поэтому имя переменной в Declare должно совпадать с ключом в json.
Например:
Запрос - `DECLARE $x1 AS Int32; SELECT $x1;`
Json - `{"$x1": 2}`

_Если вы передали в json параметры, которые не указаны в Declare, то такие параметры просто будут пропущены._
_Если вы в Declare определили ключи параметров, которые не указаны json, вы получите эксепшен._

Содержимое переменных приводится к нужному типу для YQL с помощью [Python библиотеки](https://a.yandex-team.ru/arc/trunk/arcadia/yql/library/python/yql) в зависимости от того, что вы указали в Declare. 
[Функции](https://a.yandex-team.ru/arc/trunk/arcadia/yql/library/python/yql/client/parameter_value_builder.py) из билиотеки реализуют проверки типов и их приведения к нужноми виду для YQL. [Пример](https://a.yandex-team.ru/arc/trunk/arcadia/yql/library/python/yql/api/v1/examples/parameters.py) использования этих функци.


**Шаг 4**

Отправка запросов реализована через [библиотеку](https://a.yandex-team.ru/arc/trunk/arcadia/yql/library/python/yql) YQL на python, которая реализует все нужное взаимодействие сама.

**Шаг 5**

Полученный запрос отдается на выход кубика.


### Ограничения
**Контейнеры в кубике**

Мы не поддерживаем динамическое привидение типов в [контейнерах](https://yql.yandex-team.ru/docs/yt/types/type_string#containers) из-за сложности парсинга и необязательности объявления типа внутри контейнеров каждого элемента 
Если вы используете в DECLARE контейнеры, то они не будут никак приведены и останутся в том виде, в котором вы их прислали. 
Вы можете использовать UDF или встроенные функции YQL для их конвертации (точно? надо проверить. Можно ли делать CAST? ) 
Вы можете использовать json/yson в качестве контейнера, который приведется к типу json/yson целиком.
Или вы можете попытаться расширить эту функциональность.


**Примитивные типа в кубике**

Из всех примитивных типов мы не поддерживаем только `JsonDocument`, потому что YQL библиотека на Python не имеет такой функции приведения типа.

**Опциональные типы в кубике**
Поддержаны для тех типов, что имеются в Declare, и для контейнеров. 

**Специальные типы в кубике**

Среди [специальных типов](https://yql.yandex-team.ru/docs/yt/types/special) поддержаны только Null и Void - это ограничение Declare.


### Формат передачи данных в json
YQL описывает основной формат данных [тут](https://yql.yandex-team.ru/docs/yt/types/json).

**Int8, Int16, Int32, Int64**

Эти типы данных должны быть представлены в json в виде number.

Query:
```
DECLARE $x1 AS <Int8/16/32/64>; 
SELECT $x1;
```

Json:
`{"$x1": 1}`

**Uint8, Uint16, Uint32, Uint64**

Эти типы данных должны быть представлены в json в виде number.

Query:
```
DECLARE $x1 AS <Uint8/16/32/64>; 
SELECT $x1;
```

Json:
`{"$x1": 1}`

**Bool**

Этот тип данных должен быть представлен в json в виде bool. 

Query:
```
DECLARE $x1 AS Bool;
SELECT $x1;
```
Json:
`{"$x1": false}`

**Float**

Этот тип данных должен быть представлен в json в виде number. 

Query:
```
DECLARE $x1 AS Float;
SELECT $x1;
```
Json:
`{"$x1": -1.25}`


**Double**

Этот тип данных должен быть представлен в json в виде number. 

Query:
```
DECLARE $x1 AS Float;
SELECT $x1;
```
Json:
`{"$x1": -89.76}`

**Decimal**

Этот тип данных должен быть представлен в json в виде string. 

Query:
```
DECLARE $x1 AS Decimal(22,9);
DECLARE $x2 AS Decimal(22,9);
DECLARE $x3 AS Decimal(22,9);
DECLARE $x4 AS Decimal(22,9);
SELECT $x1,2,3,4;
```
Json:
`{"$x1": "-123456789.8765432", "$x2": "Infinity", "$x3": "NaN", "$x4": "-Infinity"}`
Пока нельзя использовать "inf", "nan", "-inf", потому что библиотека python подготовки некорректно преобразует эти значения в 1.000000000000000000000000000E+36, чего yql не понимает. 
https://a.yandex-team.ru/arc/trunk/arcadia/yql/library/python/yql/client/parameter_value_builder.py?rev=r9037227#L463

Если вы пришлете decimal в number, то ваше значение не сойдется и будет представлять -123456789.8765432 -> -123456789.8765431940555572509765625.

**String**

Этот тип данных должен быть представлен в json в виде string. 

Query:
```
DECLARE $x1 AS String;
SELECT $x1;
```
Json:
`{"$x1": "aaaa"}`

А что с бинарными данными? 
Все String в YT являются бинарными данными, если вы хотите прокачать через кубик блоб, лучше этого избежать, но вы можете попробовать следуя этим [рекоментациям](https://yql.yandex-team.ru/docs/yt/types/json#string) для json. 
Мы не уверены в том, что ваши данные вставятся так, как нужно.

```
DECLARE $x1 AS String;
SELECT $x1;
```
`{"$x1": "\\u0005\\nk\\u00FF"}`

Мы не стали делать осознанно расширение этой функциональности для перекладывания именно байт, так как библиотека json в Python при сериализации пытается все данные представлять как utf-8 строки, а не байты.

Возможно вам могут быть полезны встроенные [функции](https://yql.yandex-team.ru/docs/yt/builtins/basic#to-from-bytes) ToBytes и FromBytes


**Utf8** 

Этот тип данных должен быть представлен в json в виде string. 

Query:
```
DECLARE $x1 AS Utf8;
SELECT $x1;
```
Json:
`{"$x1": "bbbb"}`

Не забывайте про эскейпинг json символов!

**Yson**

Этот тип данных должен быть представлен в json в виде string. 
Описание YSON и его грамматик можно прочитать [тут](https://wiki.yandex-team.ru/yt/internal/yson/).

Query:
```
DECLARE $x1 AS Yson;
SELECT $x1;
```
Json:
`{"$x1": "{a=123; b=aaa}"}`


**Json**

Query:
```
DECLARE $x1 AS Json;
SELECT $x1;
```
Json:
`{"$x1": {"fff": 1}}`


**Uuid**

Этот тип данных должен быть представлен в json в виде string. 

Query:
```
DECLARE $x1 AS Uuid;
SELECT $x1;
```
Json:
`{"$x1": "550e8400-e29b-41d4-a716-446655440000"}`


**Date** 

Этот тип данных должен быть представлен в json в виде string в iso формате. 
Значение будет приведено к datetime и приведено к нужному виду для YQL.

Query:
```
DECLARE $x1 AS Date;
SELECT $x1;
```
Json:
`{"$x1": "2018-02-15"}`



**Datetime** 

Этот тип данных должен быть представлен в json в виде string в iso формате. 
Значение будет приведено к datetime и приведено к нужному виду для YQL.

Query:
```
DECLARE $x1 AS Datetime;
SELECT $x1;
```
Json:
`{"$x1": "2018-02-15T15:16:17"}`


**Timestamp**

Этот тип данных должен быть представлен в json в виде string в iso формате. 
Значение будет приведено к datetime и приведено к нужному виду для YQL.

Query:
```
DECLARE $x1 AS Timestamp;
SELECT $x1;
```
Json:
`{"$x1": "2018-02-15T15:16:17.034567"}`


**Interval** 

Этот тип данных должен быть представлен в json в виде string в iso формате обернутый в list.
Второй элемент будет вычтен из первого при преобразовании.

Query:
```
DECLARE $x1 AS Interval;
SELECT $x1;
```
Json:
`{"$x1": ["2018-02-15T15:16:17", "2018-02-15T15:16:17"]}`


**TzDate/TzDatetime/TzTimestamp** 

Этот тип данных должен быть представлен в json в виде string. 

Для удобства мы никак не будем в библиотеке приводить данный тип, вы можете просто указать в ISO формате дату и через запятую указать таймзону, как того требует документация YT.

Query:
```
DECLARE $x1 AS TzDate;
DECLARE $x2 AS TzDatetime;
DECLARE $x3 AS TzTimestamp;
SELECT $x1,$x2,$x3;
```
Json:
`{"$x1": "2018-02-15,America/Los_Angeles","$x2": "2018-02-15T15:16:17,Europe/Moscow","$x3": "2018-02-15T15:16:17.034567,GMT"}`


**Void** 

Если вам нужно использовать Void то Declare, которы объявлен как Void, будет приведен к Void вне зависимости от содержимого переменной.


Query:
```
DECLARE $x1 AS Void;
SELECT $x1;
```
Json:
`{"$x1": "Void"}`


**Optional**

Поддерживаются только примитивные типы, этот тип данных должен быть представлен в json в том виде, в каком этого требует тип данных, который вы делаете опциональным. 
Все переменные в json, которые определены как Optional в Declare и являются пустой строкой или null, будут приведены к типу Null.
```
DECLARE $x1 AS Float?;
SELECT $x1;
```
Json:
```{"$x1": -1.25}```
```{"$x1": ''}```
```{"$x1": null}```


**List** 

Данный тип не поддержан и он не будет преобразован!
Value в json будет переложено без изменений. Вы сможете его привести сами либо до, либо после с помощью встроенных функций в YQL.
Этот тип данных должен быть представлен в json в виде списка.


Query:
```
DECLARE $x1 AS List<String>;
SELECT $x1;
```
Json:
```{"$x1": ["a", "b"]}```


**Struct** 

Данный тип не поддержан и он не будет преобразован!
Value в json будет переложено без изменений. Вы сможете его привести сами либо до, либо после с помощью встроенных функций в YQL.
Этот тип данных должен быть представлен в json в виде словаря.


Query:
```
DECLARE $x1 AS Struct<Id:Int64, Name:String>;
SELECT $x1;
```
Json:
```{"$x1": {"Id": "1", "Name": "Anna"}}```


**Stream** 

Данный тип не поддерживается yql для Declare!

**Variant** 

Не поддержан!


**Dict** 

Данный тип не поддержан и он не будет преобразован!
Value в json будет переложено без изменений. Вы сможете его привести сами либо до, либо после с помощью встроенных функций в YQL.
Этот тип данных должен быть представлен в json записывается в массив массивов, состоящих из двух элементов.


Query:
```
DECLARE $x1 AS Dict<Int64,String>;
SELECT $x1;
```
Json:
```{"$x1": [["1","Value"],["2","Value"]]}```


**Tuple** 

Данный тип не поддержан и он не будет преобразован!
Value в json будет переложено без изменений. Вы сможете его привести сами либо до, либо после с помощью встроенных функций в YQL.
Этот тип данных должен быть представлен в json в виде списка.


Query:
```
DECLARE $x1 AS Tuple<String, Int64>;
SELECT $x1;
```
Json:
```{"$x1": ["Some string", "64"]}```



**EmptyList** 

Данный тип не поддержан и он не будет преобразован!
Value в json будет переложено без изменений. Вы сможете его привести сами либо до, либо после с помощью встроенных функций в YQL.
Этот тип данных должен быть представлен в json в виде пустого списка.


Query:
```
DECLARE $x1 AS AS EmptyList;;
SELECT $x1;
```
Json:
```{"$x1": []}```

**EmptyDict** 

Данный тип не поддержан и он не будет преобразован!
Value в json будет переложено без изменений. Вы сможете его привести сами либо до, либо после с помощью встроенных функций в YQL.
Этот тип данных должен быть представлен в json в виде словаря.


Query:
```
DECLARE $x1 AS EmptyDict;
SELECT $x1;
```
Json:
```{"$x1": {}}```


### Примеры использования
Пример YQL-запроса с данными прогнанными через кубик - https://yql.yandex-team.ru/Operations/YoTHmq5OD-gvVPXa-BMDJt5dtzXunGjxQAM_hj1MbUo=

Запрос:
```
   DECLARE $x1 AS Int8;
    DECLARE $x2 AS Int16;
    DECLARE $x3 AS Int32;
    DECLARE $x4 AS Int64;
    DECLARE $x5 AS Uint8;
    DECLARE $x6 AS Uint16;
    DECLARE $x7 AS Uint32;
    DECLARE $x8 AS Uint64;
    DECLARE $x9 AS Bool;
    DECLARE $x10 AS Float;
    DECLARE $x11 AS Double;
    DECLARE $x12 AS Decimal(33,2);
    -- DECLARE $x121 AS Decimal(33,2); "inf"
    -- DECLARE $x122 AS Decimal(33,2); "nan"
    -- DECLARE $x123 AS Decimal(33,2); "-inf"
    DECLARE $x13 AS String;
    DECLARE $x131 AS String; --binary
    DECLARE $x14 AS Utf8;
    DECLARE $x15 AS Uuid;
    DECLARE $x16 AS Yson;
    DECLARE $x17 AS Json;
    DECLARE $x18 AS Date;
    DECLARE $x19 AS Datetime;
    DECLARE $x20 AS Timestamp;
    DECLARE $x21 AS Interval;
    DECLARE $x22 AS TzDate;
    DECLARE $x23 AS TzDatetime;
    DECLARE $x24 AS TzTimestamp;
    DECLARE $x25 AS Void;
    DECLARE $x251 AS Void;

    -- Optional
    DECLARE $x26 AS Int8?;
    DECLARE $x27 AS Int16?;
    DECLARE $x28 AS Int32?;
    DECLARE $x29 AS Int64?;
    DECLARE $x30 AS Uint8?;
    DECLARE $x31 AS Uint16?;
    DECLARE $x32 AS Uint32?;
    DECLARE $x33 AS Uint64?;
    DECLARE $x34 AS Bool?;
    DECLARE $x35 AS Float?;
    DECLARE $x36 AS Double?;
    DECLARE $x37 AS Decimal(33,2)?;
    -- DECLARE $x371 AS Decimal(33,2)?;  "inf"
    -- DECLARE $x372 AS Decimal(33,2)?;  "nan"
    -- DECLARE $x373 AS Decimal(33,2)?;  "-inf"
    DECLARE $x38 AS String?;
    DECLARE $x381 AS String?; --binary
    DECLARE $x382 AS String?; --empty
    DECLARE $x383 AS String?; --null
    DECLARE $x39 AS Utf8?;
    DECLARE $x40 AS Uuid?; -- don't work with ["GLwSGDhY3kyYqihzAml7kA=="] format
    DECLARE $x41 AS Yson?;
    DECLARE $x42 AS Json?;
    DECLARE $x43 AS Date?;
    DECLARE $x44 AS Datetime?;
    DECLARE $x45 AS Timestamp?;
    DECLARE $x46 AS Interval?;
    DECLARE $x47 AS TzDate?;
    DECLARE $x48 AS TzDatetime?;
    DECLARE $x49 AS TzTimestamp?;
    DECLARE $x50 AS Void?;
    DECLARE $x501 AS Void?;

    DECLARE $x60 AS Struct<Id:Int64, Name:String>;
    DECLARE $x601 AS Struct<Id:Int64, Name:String>?;

    DECLARE $x61 AS List<String>;
    DECLARE $x611 AS List<String>?;

    DECLARE $x62 AS Dict<Int64, String>;
    DECLARE $x621 AS Dict<Int64,String>?;

    -- DECLARE $x63 AS Variant<Int64, String>;
    -- DECLARE $x64 AS Variant<a:Int64, b:String>;

    DECLARE $x65 AS Tuple<String, Int64?>;
    DECLARE $x651 AS Tuple<String, Int64>?;

    DECLARE $x66 AS EmptyList;
    DECLARE $x661 AS EmptyList?;

    DECLARE $x67 AS EmptyDict;
    DECLARE $x671 AS EmptyDict?;

    SELECT $x1 as x1, $x2 as x2, $x3 as x3, $x4 as x4, $x5 as x5, $x6 as x6, 
    $x7 as x7, $x8 as x8, $x9 as x9, $x10 as x10, $x11 as x11, $x12 as x12, $x13 as x13, 
    $x131 as x131, $x14 as x14, $x15 as x15, $x16 as x16, $x17 as x17, $x18 as x18, 
    $x19 as x19,  $x20 as x20, $x21 as x21, $x22 as x22, $x23 as x23, $x24 as x24,  
    $x25 as x25, $x251 as x251, $x26 as x26, $x27 as x27, $x28 as x28, $x29 as x29, 
    $x30 as x30,  $x31 as x31, $x32 as x32, $x33 as x33, $x34 as x34, $x35 as x35, 
    $x36 as x36, $x37 as x37, $x38 as x38, $x381 as x381, $x382 as x382, $x383 as x383, 
    $x39 as x39, $x40 as x40, $x41 as x41, $x42 as x42, $x43 as x43, $x44 as x44, 
    $x45 as x45,  $x46 as x46, $x47 as x47, $x48 as x48, $x49 as x49, $x50 as x50, 
    $x501 as x501,  $x60 as x60, $x601 as x601, $x61 as x61, $x611 as x611, $x62 as x62,
    $x621 as x621, $x65 as x65, $x651 as x651, $x66 as x66, $x661 as x661, $x67 as x67, 
    $x671 as x671
```

Json из запроса:
```
{"$x1": 1, "$x2": 2, "$x3": 3, "$x4": 4, "$x5": 5, "$x6": 6, "$x7": 7, "$x8": 8, "$x9": false, "$x10": -1.25, "$x11": -89.76, "$x12": "-123456789.8765432", "$x121": "Infinity", "$x122": "NaN", "$x123": "-Infinity", "$x13": "aaaa", "$x131": "\\u0000\\u0001\\u0002\\u0003\\u0004\\u0005\\u0006\\u0007\\u0008", "$x14": "bbbb", "$x15": "550e8400-e29b-41d4-a716-446655440000", "$x16": "{a=123; b=aaa}", "$x17": {"b": 321}, "$x18": "2018-02-01", "$x19": "2018-02-01T15:16:17", "$x20": "2018-02-01T15:16:17.034567", "$x21": ["2018-02-01T15:16:17.034567","2018-03-02T16:17:18.123123"], "$x22": "2018-02-01,America/Los_Angeles", "$x23": "2018-02-01T15:16:17,Europe/Moscow", "$x24": "2018-02-01T15:16:17.034567,GMT", "$x25": "Void", "$x251": null, "$x26": 1, "$x27": 2, "$x28": 3, "$x29": 4, "$x30": 5, "$x31": 6, "$x32": 7, "$x33": 8, "$x34": false, "$x35": -1.25, "$x36": -89.76, "$x37": "-123456789.8765432", "$x38": "aaaa", "$x381":"\\u0000\\u0001\\u0002\\u0003\\u0004\\u0005\\u0006\\u0007\\u0008",  "$x382": "",  "$x383": null,  "$x39": "bbbb", "$x40": "550e8400-e29b-41d4-a716-446655440000", "$x41": "{a=123; b=aaa}", "$x42": {"b": 321}, "$x43": "2018-02-01", "$x44": "2018-02-01T15:16:17", "$x45": "2018-02-01T15:16:17.034567", "$x46": ["2018-02-01T15:16:17.034567","2018-03-02T16:17:18.123123"], "$x47": "2018-02-01,America/Los_Angeles", "$x48": "2018-02-01T15:16:17,Europe/Moscow", "$x49": "2018-02-01T15:16:17.034567,GMT", "$x50": "Void", "$x501": null, "$x60": {"Id": "1", "Name": "Anna"}, "$x601": {"Id": "1", "Name": "Anna"}, "$x61": ["a", "b"], "$x611": ["a", "b"], "$x62": [["1","Value"],["2","Value"]], "$x621": [["1","Value"],["2","Value"]], "$x63": [["1","Value"],["2","Value"]], "$x64": ["1", "value1"], "$x65": ["Some string", "64"], "$x651": ["Some string", "64"], "$x66": [], "$x661": [], "$x67": {}, "$x671": {}}
```

