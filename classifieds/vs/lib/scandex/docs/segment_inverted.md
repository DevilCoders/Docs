# Описание реализации InvertedSegment

Реализацией InvertedSegment в нашем проекте является PostingList.

PostingList представляет собой список пар вида `List[(ValueIdx, List[DocumentId])]`.

- N (или `documentsCount` в коде) - общее число хранимых документов
- M - количество различных возможных значений

Поддерживаются следующие операции:
- Получить документы с заданным значением поля
- Получить документы со значением большим/меньшим, чем заданное значение поля, включая/исключая
заданное значение поля
- Получить документы, имеющие то же значение(те же значения), что и документ 
под заданным номером 
- Получить документы с незаполненным значением поля

## Реализации PostingList
Для улучшения производительности и уменьшения размера индекса были реализованы два
варианта `PostingList` для обычного и [мульти-индекса](glossary.md#multi-index).
### MultiPostingList
Значения поля для каждого документа хранятся в буфере как построчно записанная 
таблица размера (M+1)*N, где значение `(i,j)` ячейки равно 0 или 1, в зависимости от 
того, равно ли данное поле в`j`-ом документе значению с `ValueIndex=i`.
В строке `(M, j)` хранится 0 в случае, если у `j`-го документа есть значения в данном поле,  или 1, в случае, если у
документа отсутствуют значения.

#### Обобщенный пример:
              
ValueIndex    | N-1 | N-2 | ... |  1  |  0
:------------:|:---:|:---:|:---:|:---:|:---:
0             |  1  |  0  | ... |  0  |  1
1             |  1  |  1  | ... |  1  |  0
...           | ... | ... | ... | ... | ...
M - 1         |  0  |  0  | ... |  0  |  1
null          |  0  |  0  | ... |  0  |  0

Чтобы узнать, для каких документов `ValueIdx = i`, нужно прочитать 
значение из буфера по `N*i` смещению. 

### BinaryRadixPostingList
Значение поля для каждого документа хранится в буфере как построчно записанная 
таблица размера `([lg M] +1) * N`, закодированная следующим образом:
0. Для значения с помощью [кодификатора значений](glossary.md#segment-values-lookup)
вычисляем `ValueIdx` - получаем число из диапазона [0, M-1]
0. Бинарное представление `ValueIdx`(т.е. десятичное число `ValueIdx` преобразуем к виду 
числа по основанию 2) записывается в столбец соответствующего документа
0. В конец таблицы добавляем строку `notNull`(состоит из 0 и 1), которая равна 1, 
если для документа проставлено значение. Данная строка необходима для разделения 
случаев нулевого столбца с проставленным `ValueIdx = 0` и неустановленного значения(см. DocumentId=0 и 
DocumentId=6 в [примере](#single-example)
).

Переход к бинарному представлению позволяет: 
- уменьшить количество строк и тем самым сократить размер буфера
- эффективно осуществлять поиск по буферу

#### <a id="single-example" /> Пример схемы кодирования для `M=6` и `N=7`: [&dHar;](#single-example)
Максимальное значение `ValueIdx` = (6-1) = 5 = 101b. Следовательно, для кодирования шести 
значений достаточно 3 строки + `null` строка.

|  6  |  5  |  4  |  3  |  2  |  1  |  0
|:---:|:---:|:---:|:---:|:---:|:---:|:---:
|  0  |  1  |  1  |  0  |  0  |  0  |  0
|  0  |  0  |  0  |  1  |  1  |  1  |  0
|  0  |  1  |  0  |  0  |  0  |  1  |  0
|  0  |  0  |  0  |  0  |  0  |  0  |  1
  
 Фактическое соответствие между документами и значением:
 
 ValueIdx | List(DocumentId) 
 :-------:|:----------------:
 0        | 6
 1        | 
 2        | 2,3
 3        | 1
 4        | 4
 5        | 5
 -1       | 0
 
Чтобы узнать, для каких документов значение данного поля равно `i`, нужно найти столбец, 
равный (i(в бинарном представлении),1). 

Похожая схема кодирования, используемая в **Pilosa**, более подробно описана [тут](https://www.pilosa.com/blog/range-encoded-bitmaps/).

[cardinality]: glossary.md#cardinality
