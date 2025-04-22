# Глоссарий scandex

### <a id="document" /> Документ [&dHar;](#document)
"Строка" в терминах баз данных. Объединение значений полей с уникальным [первичным ключом](#pk).

### <a id="pk" /> Первичный ключ [&dHar;](#pk)
Внешний идентификатор [документа](#document). Должен быть уникален в пределах [базы данных](#database).
Внутреннее устройство индексов, хранящих первичный ключ, описывается в [соответствующем разделе документации](primary.md)

### <a id="database" /> База данных [&dHar;](#database)
Набор уникальных однородных [документов](#document). Состоит из одного и более [шардов](#shard).

### <a id="shard" /> Шард [&dHar;](#shard)
Набор уникальных документов, сгруппированных относительно некоторой хэш-функции. Шард состоит из [индексов](#index) полей.
Каждый [документ](#document) имеет внутренний номер в рамках этого шарда - `DocumentId`.

### <a id="field" /> Поле [&dHar;](#field)
[Типизированное](#types) свойство документа, хранящееся в [индексе](#index).

### <a id="types" /> Типы данных [&dHar;](#types)
| Тип данных     | [pk](#pk) | [range](#ops-range) | [filter](#ops) | [store](#index-storage) |
|----------------|-----------|---------------------|----------------|-------------------------|
| `Boolean`      | &check;   | &check;             | &check;        | &check;                 |
| `Byte`         | &check;   | &check;             | &check;        | &check;                 |
| `Short`        | &check;   | &check;             | &check;        | &check;                 |
| `Int`          | &check;   | &check;             | &check;        | &check;                 |
| `Long`         | &check; |&check;             | &check;        | &check;                 |
| `Float` <sup>[1](#fp-ordering)</sup>  | &cross;        | &check; | &check; | &check;       |
| `Double` <sup>[1](#fp-ordering)</sup> | &cross;        | &check; | &check; | &check;       |
| `Char`         | &check;   | &check;             | &check;        | &check;                 |
| `String` <sup>[2](#charset)</sup> <sup>[3](#array-ordering)</sup> | &check; | &check; | &check; | &check; |
| `Array[Byte]` <sup>[3](#array-ordering)</sup>| &cross; | &check; | &check; | &check;       |
| `Set[?]`       | &cross;   | &cross;             | &check; <sup>[4](#set-note)</sup> | &check; |
| `T: Serde`     | &cross;   | &cross;             | &cross;        | &check;                 |

<a id="fp-ordering">`1`</a> Числа с плавающей точкой сравниваются в соответствии с [тотальным компаратором](https://scala-lang.org/api/2.13.x/scala/math/Ordering$$Double$$TotalOrdering.html)

<a id="charset">`2`</a> Строки могут быть только в кодировке `UTF-8`

<a id="array-ordering">`3`</a> Строки и массивы сравниваются побайтово начиная с первого байта

<a id="set-note">`4`</a> Только для типов, которые могут быть отфильтрованы

### <a id="index" /> Индекс [&dHar;](#index)
Композиция структур данных, хранящая поля документов. Может быть [хранящим](#index-storage), [фильтрующим](#index-filter) и [диапазонным](#index-range).

Индекс состоит из сегментов. Сегменты - это сериализованные представления структур данных, используемых для поиска и хранения значений в индексе.

#### <a id="index-filter" />Фильтрующий индекс
Позволяет фильтровать [документы](#document). Фильтрующий индекс может строиться для одного или для набора значений у документа. Наличие значения у документа опционально. Реализует операции [равенство](#ops-equals), [принадлежность к множеству](#ops-in) и [отсутствие значения](#isNull).

#### <a id="index-range" />Диапазонный индекс
Позволяет фильтровать [документы](#document) по [принадлежности к диапазону](#ops-range). Может содержать только одно значение для документа, либо же не содержать никакого.

#### <a id="index-storage" />Хранящий индекс
Позволяет получить значение [документа](#document) по его `DocumentId`.

### <a id="logic-ops" /> Логические операции [&dHar;](#logic-ops)
На данный момент scandex реализует операции [булевой алгебры](https://ru.wikipedia.org/wiki/%D0%91%D1%83%D0%BB%D0%B5%D0%B2%D0%B0_%D0%B0%D0%BB%D0%B3%D0%B5%D0%B1%D1%80%D0%B0) для комбинации подзапросов. Примитивный оптимизатор позволяет упростить некоторые запросы используя [свойства булевой алгебры](https://ru.wikipedia.org/wiki/%D0%91%D1%83%D0%BB%D0%B5%D0%B2%D0%B0_%D0%B0%D0%BB%D0%B3%D0%B5%D0%B1%D1%80%D0%B0#%D0%9D%D0%B5%D0%BA%D0%BE%D1%82%D0%BE%D1%80%D1%8B%D0%B5_%D1%81%D0%B2%D0%BE%D0%B9%D1%81%D1%82%D0%B2%D0%B0).
```scala
import MySchema._
(ToBe === true | !ToBe === true) == Everything // true оптимизация!
```

#### <a id="logical-ops-and" /> `and, &` [&dHar;](#logical-ops-and)
Вернёт документы, которые найдутся для левого **И** одновременно правого подзапросов.
```scala
import MySchema._
Dazed === true & Confused === true
```

#### <a id="logical-ops-or" /> `or, |` [&dHar;](#logical-ops-or)
Вернёт все документы, которые соответствуют левому **ИЛИ** правому подзапросу.
```scala
import MySchema._
ChairWithS === false | ChairWithD === false
```

#### <a id="logical-ops-not" /> `not, !q, ~q` [&dHar;](#logical-ops-not)
Вернёт все документы, которые **НЕ** соответствуют подзапросу.
```scala
val query = MySchema.CovidProbability <= 1
!query == MySchema.CovidProbability > 1 // true
~query     // same
not(query) // also same
query.not  // goddammit, the same!
```

### <a id="ops" /> Операции сравнения [&dHar;](#ops)
Корень всех запросов. Комбинируются с помощью логических операций. Определены для [фильтрующих](#index-filter) и [диапазонных](#index-range) [индексов](#index), если ниже не сказано иначе.

#### <a id="ops-equals" /> `===` [&dHar;](#ops-equals)
Равенство. Возвращает документы которые содержат в [поле](#field) ключ.
```scala
MySchema.MyIntField === 1
```

#### <a id="ops-in" /> `in, <=>` [&dHar;](#ops-in)
Принадлежность к множеству. Возвращает документы, которые содержат хотя бы один из перечисленных ключей.
```scala
MySchema.RegionId in (1, 213)
MySchema.Rhyme <=> ("Stay", "the", "f**k", "at", "home")
```

#### <a id="is-null" /> `isNull` [&dHar;](#is-null)
Отсутствия значения. Возвращает документы, которые не имеют ни одного значения в поле.
```scala
MySchema.Future.isNull
```

#### <a id="ops-range" /><a id="ops-less-than" /> `lessThan, <, <=` [&dHar;](#ops-range)
#### <a id="ops-greater-than" /> `greaterThan, >, >=` [&dHar;](#ops-greater-than)
#### <a id="ops-between" /> `between, <=<` [&dHar;](#ops-between)
Вхождение в диапазон. Возвращает документы, значения в которых [меньше](#ops-less-than), [больше](#ops-greater-than) (или равны), либо находятся [между двумя ключами включительно](#ops-between). Определены только для [диапазонного](#index-range) [индекса](#index).
```scala
import MySchema._
OilPrice < 0
Credit <= 10
USDRate >= 80
Weekday >= "Пятница"
Confidence <=< (0, 0.1)
Price between 1000 and 3000
```

### <a id="segment" /> Сегмент [&dHar;](#segment)
Сериализованное представление структуры данных, используемой в [индексе](#index). На текущий момент определены следующие назначения сегментов:

#### <a id="segment-forward" /> Прямой индекс [&dHar;](#segment-forward)
`DocumentId -> Seq[ValueIdx]` (`Seq` - для случая когда поле документа - список значений).   
Умеет отвечать на вопрос "какие значения соответствуют документу". Представляет собой последовательность `ValueIdx`, 
позиция которых есть `DocumentId`. Реализация описана в [соответвующем документе](segment_forward.md)

#### <a id="segment-values-lookup" /> Кодификатор значений [&dHar;](#segment-values-lookup)
`FieldValue -> ValueIdx`  
Хранит привязку значения поля к ValueIdx, умеет находить ValueIdx по значению поля документа. В ряде реализаций 
является также [хранилищем значений](#segment-values-storage).

#### <a id="segment-values-storage" /> Хранилище значений [&dHar;](#segment-values-storage)
`ValudeIdx -> FieldValue`  
Хранит значения поля документа. Умеет находить значение поля документа по ValueIdx. В отличие 
от [набора значений](#segment-values), не может быть использован для поиска по значению поля.

#### <a id="segment-inverted" /> Инвертированный индекс [&dHar;](#segment-inverted)
`ValueIdx -> Seq[DocumentId]`  
Содержит в себе набор соответствий документов значениям. Отвечает на вопрос "какие документы содержат в себе это значение. Порядковый номер значения соответствует таковому в [наборе значений](#segment-values)
Реализация описана в [соответвующем документе](segment_inverted.md)

#### <a id="multi-index" /> Мульти-индекс [&dHar;](#multi-index)
Характеристика [прямого](#segment-forward) или [инвертированного](segment-inverted) 
индекса, обозначающая, что его реализация позволяет установить для одного документа сразу
несколько значений поля. Иначе индекс называется просто **индекс** или **обычный индекс**
#### <a id="cardinality" /> cardinality() [&dHar;](#log-size-of)

Функция, возвращающая размер применимого для размещения данного количества значений типа:

```scala
  def cardinality(v: Long): Byte =   
    if (v < 256) 1              // 2^8
    else if (v < 65536) 2       // 2^16
    else if (v <= 4294967296) 4 // 2^32
    else 8 
```

### Пример

Для запроса
```sql
SELECT price
FROM db
WHERE mark = "AUDI"
```
Проход по сегментам будет выглядеть примерно так:
1) `fieldValue ("AUDI") -> valueIdx` // кодификатор значений
2) `valueIdx -> Seq[DocumentId]` // инвертированный индекс
3) `DocumentId -> ValueIdx (price)` // прямой индекс
4) `valueIdx -> fieldValue (price as double)` // хранилище значений
