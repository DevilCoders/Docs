# D

В данном разделе приведено описание метрик, первой буквой в названии которой является <q>D</q> (без учета [оцененности](naming.md#judged)). {#list}

## diff-2-serps {#diff-2-serps}

Количество документов, которые отличаются в [соседнем SERP](../reference/term.md#neighbor-serp). 

[К списку метрик](#list).


## diff-2-serps-newdoc {#diff-2-serps-newdoc}

Количество документов, которые отсутствуют в [соседнем SERP](../reference/term.md#neighbor-serp).

Например, при сравнении Яндекса и Гугла значение <q>24</q> для Яндекса означает, что в выдаче Яндекса в среднем 24 документа на запрос, которые не отражены в поисковой выдаче Гугла.

Особенности в интерфейсе:

- Если документ найден в обоих сравниваемых SERP, то отражается его позиция в текущем и сравниваемом SERP в формате: <q>1 → 24</q>. Первое число (1) отражает позицию документа в текущем серпе, второе (24) — в том, с которым проводится сравнение.
- Если документ отсутствует в соседнем SERP, то ему ставится метка <q>new</q>.

{% include [diff-2-serps-backtolist](../_includes/concepts/d/id-diff-2-serps/backtolist.md) %}



## diff-coordinate-2-serps {#diff-coordinate-2-serps}

Количество точек на карте, которые отсутствуют в [соседнем SERP](../reference/term.md#neighbor-serp). Cравнение проводится по координатам точки.

Например, при сравнении Яндекса и Гугла значение <q>20</q> для Яндекса означает, что в выдаче Яндекса в среднем 20 точек на карте, которые не отражены в поисковой выдаче Гугла.

Особенности в интерфейсе:

- Если точка на карте найдена в обоих сравниваемых SERP, то отражается ее позиция в текущем и сравниваемом SERP в формате: <q>1 → 24</q>. Первое число (1) отражает позицию точки в текущем SERP, второе (24) — в том, с которым проводится сравнение.
- Если точка отсутствует в соседнем SERP, то ей ставится метка <q>new</q>.

{% include [diff-2-serps-backtolist](../_includes/concepts/d/id-diff-2-serps/backtolist.md) %}



## diff-judged-click-authority {#diff-judged-click-authority}

Разница в количестве документов на SERP, для которых известна кликовая добавка, и документов с предсказанной авторитетностью.

### Расчет метрики {#diff-judged-click-authority}

Значение метрики равно модулю разности метрик **judged-click** и **judged-authority**:

$diff{-}judged{-}click{-}authority = |judged{-}click - judged{-}authority|$
 
{% include [diff-2-serps-backtolist](../_includes/concepts/d/id-diff-2-serps/backtolist.md) %}



## docs-found {#docs-found}

Количество найденных по запросу документов.

{% include [diff-2-serps-backtolist](../_includes/concepts/d/id-diff-2-serps/backtolist.md) %}



## duplicate-images {#duplicate-images}

Доля картинок, имеющих дубликаты в первых n результатах поисковой выдачи.

### Расчет метрики {#duplicate-images}

Значение метрики равно сумме отношений картинок с дубликатами, размещенными выше в поисковой выдаче, к общему числу документов (n).
 $duplicate{-}images = \sum\limits_{i=1}^{n} \frac{DupsBefore_i > 0}{n} { ,}$
 
где:

1. $DupsBefore_i > 0$ — число картинок, дубликаты которых расположены перед ними в поисковой выдаче;
1. $n$ — общее число документов в выдаче.

{% include [diff-2-serps-backtolist](../_includes/concepts/d/id-diff-2-serps/backtolist.md) %}


