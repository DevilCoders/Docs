# T

В данном разделе приведено описание метрик, первой буквой в названии которой является <q>T</q> (без учета [оцененности](naming.md#judged)). {#list}

## tcg (3CG) {#tcg}

Оценка ранжирования на основе релевантности, кликовой добавки и предсказанной авторитетности документов поисковой выдачи.

### Расчет метрики {#tcg-calc}

Метрика вычисляется по формуле:

$tcg = \sum\limits_{i=0}^{n} (relevance_{i} + 0,17 * pclicks_{i} + 0,03 * authority_{i}) * \frac{1}{1 + i} { ,}$
 
где:

* $i$ — позиция документа в выдаче;
* $relevance_{i}$ — [значение релевантности](#tcg-p-rel) $i$-го результата выдачи;
* $pclicks_{i}$ — [значение кликовой добавки](#pclicks0) для $i$-ого результата выдачи;
* $authority_{i}$ — [предсказанная авторитетность](#authority0) для $i$-ого результата выдачи.

Значение кликовой добавки ($pclicks_{i}$) поступает из массива `SearcherProp`. Источники: {#pclicks0}

- основной: фактор ``WEB.FormulaValueDump_click``;
    
- альтернативный (если нет данных в основном): фактор `WEB_MISSPELL.FormulaValueDump_click`.
    

При отсутствии факторов в обоих источниках, значение $pclicks_{i}=0$

Значение предсказанной авторитетности ($authority_{i}$) поступает из массива `SearcherProp`. Источники: {#authority0}

- основной: фактор `WEB.FormulaValueDump__tw`;
    
- альтернативный (если нет данных в основном): фактор `WEB_MISSPELL.FormulaValueDump__tw`.
    

При отсутствии факторов в обоих источниках, значение $authority_{i}=0$.

При расчете метрики используются следующие значения релевантности оцененных документов ($relevance_{i}$): {#tcg-p-rel}

**Типы оценки релевантности** | **Значение**
----- | -----
Витальный (V) | 0,28
Полезный (U) | 0,21
Релевантный плюс (R+) | 0,14
Релевантный минус (R-) | 0,07
Нерелевантный (IR) | 0,0


[К списку метрик](#list).


## tcg-tw-real {#tcg-tw-real}

Оценка ранжирования на основе релевантности, кликовой добавки и асессорской авторитетности по первым n документам выдачи.

### Расчет метрики {#tcg-tw-real-calc}

Метрика вычисляется по формуле:

$tcg{-}tw{-}real = \sum\limits_{i=0}^{n} (relevance_{i} + 0,17 * pclicks_{i} + 0,03 * authority_{i}) * \frac{1}{1 + i} { ,}$
 
где:

* $i$ — позиция документа в выдаче;
* $relevance_{i}$ — [значение релевантности](#tcg-tw-real-p-rel) $i$-го результата выдачи;
* $pclicks_{i}$ — [значение кликовой добавки](#pclicks4) для $i$-ого результата выдачи;
* $authority_{i}$ — асессорская авторитетность для $i$-ого результата выдачи. Определяется по [шкале доверия TRUSTWORTHINESS](https://wiki.yandex-team.ru/trustworthiness#shkalaocenki):

**Типы оценки по шкале доверия** | **Значение**
----- | -----
Высочайшее доверие (HIGHEST) | 0,4
Высокое доверие (HIGH) | 0,3
Среднее доверие (MIDDLE) | 0,2
Низкое доверие (LOW) | 0,1
Отрицательное доверие (LOWEST) | 0
404 | 0


{% include [tcg-pclicks0](../_includes/concepts/t/id-tcg/pclicks0.md) %}
 

- основной: фактор ``WEB.FormulaValueDump_click``; {#pclicks4}
    
- альтернативный (если нет данных в основном): фактор `WEB_MISSPELL.FormulaValueDump_click`.
    

{% include [tcg-pclicks3](../_includes/concepts/t/id-tcg/pclicks3.md) %}


При расчете метрики используются следующие значения релевантности оцененных документов: {#tcg-tw-real-p-rel}

{% include [tcg-tcg-table-rel](../_includes/concepts/t/id-tcg/tcg-table-rel.md) %}


{% include [tcg-backtolist](../_includes/concepts/t/id-tcg/backtolist.md) %}



## tcgu (3CGU) {#tcgu}

Оценка ранжирования на основе релевантности документов выдачи, кликовой добавки и предсказанной авторитетности, учитывающая штраф для документов в [разгруппировке](../reference/term.md#ungroup).

### Расчет метрики {#tcgu-calc}

Метрика вычисляется по формуле:

$tcgu = \sum\limits_{i=0}^{n} \frac{relevance_{i} * /left[ /beta^i /right]^k + 0,17 * pclicks_{i} + 0,03 * authority_{i} * /left[ /beta^i /right]^k}{1 + i} { ,}$
 
где:

* $i$ — позиция документа в выдаче;
* $relevance_{i}$ — [значение релевантности](#tcgu-p-rel) $i$-го результата выдачи;
* $/left[ /beta^i /right]^k$ — коэффициент штрафа за разгруппировку: $/beta = 0,8$, $k = 0$ (если документ не принадлежит разгруппировке), $k = 1$ (если документ принадлежит разгруппировке);
* $pclicks_{i}$ — [значение кликовой добавки](#pclicks1) для $i$-ого результата выдачи;
* $authority_{i}$ — предсказанная авторитетность для $i$-ого результата выдачи.

{% include [tcg-authority0](../_includes/concepts/t/id-tcg/authority0.md) %}


- основной: фактор `WEB.FormulaValueDump__tw`;
    
- альтернативный (если нет данных в основном): фактор `WEB_MISSPELL.FormulaValueDump__tw`.
    

{% include [tcg-authority3](../_includes/concepts/t/id-tcg/authority3.md) %}


{% include [tcg-pclicks0](../_includes/concepts/t/id-tcg/pclicks0.md) %}


- основной: фактор ``WEB.FormulaValueDump_click``; {#pclicks1}
    
- альтернативный (если нет данных в основном): фактор `WEB_MISSPELL.FormulaValueDump_click`.
    

{% include [tcg-pclicks3](../_includes/concepts/t/id-tcg/pclicks3.md) %}


При расчете метрики используются следующие значения релевантности оцененных документов: {#tcgu-p-rel}

{% include [tcg-tcg-table-rel](../_includes/concepts/t/id-tcg/tcg-table-rel.md) %}


{% include [tcg-backtolist](../_includes/concepts/t/id-tcg/backtolist.md) %}



## two-cg (2CG) {#two-cg}

Оценка ранжирования на основе релевантности документов выдачи и асессорской авторитетности.

### Расчет метрики {#two-cg-calc}

Метрика вычисляется по формуле:

$two{-}cgu = \sum\limits_{i=0}^{n} \frac{0,964 * relevance_{i} + 0,036 * authority_{i}}{1 + i} { ,}$
 
где:

* $i$ — позиция документа в выдаче;
* $relevance_{i}$ — [значение релевантности](#two-сg-p-rel) $i$-го результата выдачи;
* $authority_{i}$ — асессорская авторитетность для $i$-ого результата выдачи. Определяется по [шкале доверия TRUSTWORTHINESS](https://wiki.yandex-team.ru/trustworthiness#shkalaocenki):

**Типы оценки по шкале доверия** | **Значение**
----- | -----
Высочайшее доверие (HIGHEST) | 1
Высокое доверие (HIGH) | 0,75
Среднее доверие (MIDDLE) | 0,5
Низкое доверие (LOW) | 0,25
Отрицательное доверие (LOWEST) | 0
404 | 0


При расчете метрики используются следующие значения релевантности оцененных документов: {#two-сg-p-rel}

{% include [tcg-tcg-table-rel](../_includes/concepts/t/id-tcg/tcg-table-rel.md) %}



## two-cgu (2CGU) {#two-cgu}

Оценка ранжирования на основе релевантности документов выдачи и асессорской авторитетности, учитывающая штраф для документов в [разгруппировке](../reference/term.md#ungroup).

### Расчет метрики {#two-cgu-calc}

Метрика вычисляется по формуле:

$two{-}cgu = \sum\limits_{i=0}^{n} \frac{0,964 * relevance_{i} * /left[ /beta^i /right]^k + 0,036 * authority_{i} * /left[ /beta^i /right]^k}{1 + i} { ,}$
 
где:

* $i$ — позиция документа в выдаче;
* $relevance_{i}$ — [значение релевантности](#two-cgu-p-rel) $i$-го результата выдачи;
* $/left[ /beta^i /right]^k$ — коэффициент штрафа за разгруппировку: $/beta = 0,8$, $k = 0$ (если документ не принадлежит разгруппировке), $k = 1$ (если документ принадлежит разгруппировке);
* $authority_{i}$ — асессорская авторитетность для $i$-ого результата выдачи. Определяется по [шкале доверия TRUSTWORTHINESS](https://wiki.yandex-team.ru/trustworthiness#shkalaocenki):

**Типы оценки по шкале доверия** | **Значение**
----- | -----
Высочайшее доверие (HIGHEST) | 1
Высокое доверие (HIGH) | 0,75
Среднее доверие (MIDDLE) | 0,5
Низкое доверие (LOW) | 0,25
Отрицательное доверие (LOWEST) | 0
404 | 0


При расчете метрики используются следующие значения релевантности оцененных документов: {#two-cgu-p-rel}

{% include [tcg-tcg-table-rel](../_includes/concepts/t/id-tcg/tcg-table-rel.md) %}


{% include [tcg-backtolist](../_includes/concepts/t/id-tcg/backtolist.md) %}


