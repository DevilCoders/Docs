## Описание VSQL

Запрос состоит из двух блоков:
- (опциональный) предварительный для деклараций и присваиваний значений
  - формулам ранжирования
  - примитивам и векторам
- скрипт

### Синтаксис предварительного блока

Все объявленные сущности этого блока можно упоминать и использовать внутри скрипта.

#### Формулы

Для использования формулы внутри скрипта необходимо создать из полей, алиасов, 
констант примитивных типов и результатов скалярных функций и простейших арифметических операций (+, -, *).

```sql
$by_date = 0.7 * publish_date +  1.5 * price + 2.7 * time;
```

#### Примитивы и вектора

Можно объявить константы (без указания типа, выведется автоматически исходя из значения и области применения):
```sql
$vector = (1.2, 0.0, 0.8, 1.1);
$default_price = 1000000;
$dealer_name = "ROLF";
$from_direct = true;
```
Для шаблонных запросов нужно объявить переменные:
```sql
DECLARE $description AS String;
```
Фактические значения будут передаваться в другом поле grpc-запроса рядом с vsql-запросом.

### Структура скрипта
```sql
SELECT [*] [field_1 [AS <name_1>], ...], [aggregate_func(field_1, ... ), ...],  [func(field_1, ... ), ...]
FROM <domain>
[WHERE <CONDITIONS>]
[ORDER BY <formula_1>]
[LIMIT <Int> OFFSET <Int>] 
[GROUP BY {<field_1>,...} REPRESENTED BY (HEAD | SIZE) ]
```
где
`*` - pk,modifiedAt, version и все [RawField](https://github.com/YandexClassifieds/schema-registry/blob/c2c82a9a4168427a3f655ae424fcc7c1ccb81887/proto/vertis/vasgen/document.proto#L58)

`<field_1>` - поле документа RawDocument, объявленное как [RawField](https://github.com/YandexClassifieds/schema-registry/blob/c2c82a9a4168427a3f655ae424fcc7c1ccb81887/proto/vertis/vasgen/document.proto#L58)

`<name_1>` - алиас для поля: строка, состоящая их латинских букв, цифр и знака "_"

`<domain>` - имя сервиса, например, general или auto

`<formula_1>` - объявленная в первом блоке формула для ранжирования.

```
<CONDITIONS> := CONDITION {(AND | OR) CONDITION }
<CONDITION> := (field_1 = <VALUE> | field_1 != <VALUE> | field_1 < <VALUE> | field_1 <= <VALUE> | field_1 > <VALUE> | field_1 >= <VALUE> | field_1 in ( <VALUE>, [<VALUE>,...])) 
<VALUE> := String | Int | Double | Bool | Timestamp
```

#### Скалярные функции `func`

- dot_product(doc_vector, query_vector) - модуль скалярного произведения вектора `doc_vector` из поля [embedded_vectors](https://github.com/YandexClassifieds/schema-registry/blob/c2c82a9a4168427a3f655ae424fcc7c1ccb81887/proto/vertis/vasgen/document.proto#L64)
на `query_vector`, указанный в блоке деклараций. 

#### Агрегатные функции `aggregate_func`

- `COUNT(field_1)` - количество записей поля `field_1` в группе
- `MIN(field_1)` - минимальный элемент поля `field_1` в группе
- `MAX(field_1)` - максимальный элемент поля `field_1` в группе
- `SUM(field_1)`- сумму всех значений поля `field_1` в группе
- `TOP_N(N, field_1, [field_2,...])` - первые `N` значений (или все, если значений меньше `N`) поля `field_1` (и последующих полей, если указаны). При отсутствии `N` (или =0) - все значения.

Если группировка отсутствует, то вся выборка считается одной группой. 
Все документы с отсутствующим значением поля, по которому осуществляется группировка, попадают в одну группу. 

### Типы данных

- Примитивы: String  | Int | Double | Boolean
- Вектор

### Примеры

- Листинг: запрос и ответ для стандартного поиска (фильтр + формула + лимит)

**Запрос**: все Opel'и не старше 2019
```sql
$relevance_poly = 0.7 * publish_date +  1.5 * price + coef * MAX(price);

SELECT snippet AS listing
FROM auto
WHERE year >= 2019 AND mark = "Opel"
ORDER BY relevance_poly
LIMIT 20 OFFSET 40
```
**Ответ**: 

| listing|
|--------|
|snippet1 |
|snippet2|

- Статистика: максимальная цена среди документов, удовлетворяющая фильтру

**Запрос**: максимальная цена на машины оранжевого или красного цвета не старше 2019
```sql
$relevance_poly = 0.7 * publish_date +  1.5 * price + coef * MAX(price);

SELECT MAX(price) AS max_price
FROM auto
WHERE year >= 2019 AND (color = "red" OR color = "orange")
ORDER BY relevance_poly
```
**Ответ**: число

| listing    |
|------------|
|  370000000 |

- Группировка: группируем документы по продавцу, вернуть все сниппеты группы
  
**Запрос**
```sql
$relevance_poly = 0.7 * publish_date +  1.5 * price + coef * MAX(price);

SELECT MIN(price) AS minimum, TOP_N(snippet) as docs
FROM auto
WHERE year >= 2019 AND mark = "Mercedes"
ORDER BY relevance_poly
GROUP BY seller 
```
**Ответ**

| minimum| docs|
|--------|----|
|1200000|```[snippet11, snippet12...]``` |
|3400000|```[snippet12, snippet22, snippet23,...]``` |


- Фасеты по продавцу.
Хотим понять по запросу у какого продавца сколько мерседесов в наличии.

**Запрос**: сколько машин Mercedes у каждого продавца в наличии
```sql
$relevance_poly = 0.7 * publish_date +  1.5 * price + coef * MAX(price);
$mers = "Mercedes";

SELECT seller, COUNT(in_stock) AS in_stock
FROM auto
WHERE in_stock = true AND mark = $mers
ORDER BY relevance_poly
GROUP BY seller
```
**Ответ**

| seller| in_stock|
|--------|--------|
|Авилон  |   12   |
|Панавто |   3    |
