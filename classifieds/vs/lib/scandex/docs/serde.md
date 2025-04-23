# Десериализация

Сегменты в индексах с **примитивными** значениями:

| Индекс                   | value |offset |forward|posting|count|
|--------------------------|-------|-------|-------|-------|-----|
|IntegralPrimaryIndex      |&check;|   	   |       |	   |  1  |                          
|SingleValueStorage        |&check;|	   |&check;|   	   |  2  |
|MultiValuesStorage        |&check;|&check;|&check;|   	   |  3  |
|SingleValueRangeIndexImpl |&check;|	   |&check;|&check;|  3  |
|SingleValueFilterIndex    |&check;|	   |&check;|&check;|  3  |
|MultiValuesFilterIndex    |&check;|&check;|&check;|&check;|  4  |


Сегменты в индексах со **строковыми** значениями:

| Индекс                   | value |string_offset|offset |forward|posting|count|
|--------------------------|-------|-------------|-------|-------|-------|-----|
|IntegralPrimaryIndex      |&check;|   &check;	 | 	     |   	 |	     |  2  |                          
|SingleValueStorage        |&check;|   &check;	 |	     |&check;|   	 |  3  |
|MultiValuesStorage        |&check;|   &check;	 |&check;|&check;|   	 |  4  |
|SingleValueRangeIndexImpl |&check;|   &check;   |	     |&check;|&check;|  4  |
|SingleValueFilterIndex    |&check;|   &check;   |	     |&check;|&check;|  4  |
|MultiValuesFilterIndex    |&check;|   &check;   |&check;|&check;|&check;|  5  |

# Сериализация индексов
Нeader индекса:
- тип индекса IndexType
- тип значений PlainType
- кардинальность значений: Single/Multi
- порядок байтов ByteOrdering
- количество документов docCount

## Сериализация сегментов

### Forward Segment

### Single
 - _[index] docCount_

| 🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩   | 
|-------------------------------|
| `docCount` значений типа`Long`|

### Multi

- _[index] docCount_
- totalValuesCount = offsets.last

| offsets                        | values                                       |
|--------------------------------|----------------------------------------------|
| 🟩🟩🟩🟩🟩🟩🟩🟩               | 🟨🟨🟨🟨🟨🟨🟨🟨🟨🟨🟨🟨🟨                   |
| `docCount` значений типа`Long` | `totalValuesCount + 1` значений типа  `Long` |

## Posting List 

### Single
- _[index] docCount_
- maxValueIdx
- bits

| bitmap                                         | nonnull                                  |
|------------------------------------------------|------------------------------------------|
| 🟩🟩🟩 🟩🟩🟩 🟩🟩🟩 🟩🟩🟩 🟩🟩🟩 🟩🟩🟩        | 🟨🟨🟨🟨🟨🟨🟨               |
| `bits ✕ ceil(docCount/64)` значений типа`Long` | `ceil(docCount/64)` значений типа  `Long` |

### Multi

- _[index] docCount_
- maxValueIdx

| 🟩🟩🟩  🟩🟩🟩  🟩🟩🟩  🟩🟩🟩  🟩🟩🟩  🟩🟩🟩             | 
|------------------------------------------------------------|
| `(maxValueIdx + 1) ✕ ceil(docCount/64)` значений типа`Long` |

## Value Segment
### Bitset
- bits

| 🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩  | 
|-------------------------------------|
| `ceil(bits/64)` значений типа`Long` |

### Примитив типа `T`
- _[index] тип`T`_
- numOfValues

| 🟦🟦🟦🟦🟦🟦🟦🟦🟦🟦🟦🟦🟦       | 
|----------------------------------|
| `numOfValues` значений типа `T`<sup>1</sup>|

<sup>1</sup> исключение - примитивы `Boolean`: хранятся как `Byte`


### Байты и строки
- numOfValues
- totalBytesCount = offsets.last

| offsets                           | values                                  |
|-----------------------------------|-----------------------------------------|
| 🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩          | 🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧🟧      |
| `numOfValues` значений типа`Long` | `totalBytesCount` значений типа  `Byte` |