# Реализация ForwardSegment

Прямой индекс отвечает на вопрос, какой значимый `ValueIdx` соответствует 
заданному `DocumentId`.

Для обычного и мульти индекса реализации различаются.

## Внутреннее устройство различных реализаций

Для **документов с единственным значением поля** достаточно одного сегмента памяти типа `Sequence[Long]`, в котором в _i_-ой ячейке 
хранится `ValueIdx` _i_-го документа. Кардинальность последовательности равна количеству документов. При этом специальное значение
`ValueIdx(-1L)` означает, что поле не имеет значения.

ForwardSegment для **документов с несколькими значениями поля** состоит из двух сегментов памяти типа Sequence[Long]:
 - values - плоский список значений всех документов в порядке номеров документов.
 - offsets - список смещений значений. В _i_-й ячейке хранится номер ячейки в `values`, с которой начинаются значения _i_-го документа.
   Возрастающая последовательность, всегда начинается с нуля.
   Кардинальность последовательности равна (количеству документов + 1). Последнее значение в `offsets` не ассоциировано 
   с каким-либо документом, но обеспечивает возможность определить количество значений для последнего документа.  
   
### Пример.
   Некоторый сегмент для документов с несколькими значениями поля выглядит следующим образом: 

- values
  
  | i       | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10| 11|
  |:-------:|---|---|---|---|---|---|---|---|---|---|---|---|
  | valueIdx| 0 | 1 | 2 | 0 | 0 | 2 | 3 | 1 | 3 | 0 | 2 | 3 |

- offsets:

  | i       | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
  |:-------:|---|---|---|---|---|---|---|---|---|
  | valueIdx| 0 | 3 | 3 | 4 | 5 | 5 | 7 | 9 | 12|

Это значит, что:


значения 1-го документа начинается с 3-й позиции в values
значения 2-го документа начинаются с 3-й позиции в values ⇒ у 1-го документа нет ни одного значения

значения 3-го документа начинаются с 4-й позиции в values 
значения 4-го документа начинаются с 5-й позиции в values ⇒ у 3-го документа одно значение равное 0

значения 5-го документа начинаются с 5-й позиции в values 
значения 6-го документа начинаются с 7-й позиции в values ⇒ у 5-го документа два значения равные 2 и 3.
