# C

В данном разделе приведено описание метрик, первой буквой в названии которой является <q>C</q> (без учета [оцененности](naming.md#judged)).

## click-hyp-cg {#click-hyp-cg}

Оценка поисковой выдачи на основе значения кликовой добавки (компонента $pclicks_{i}$ метрики [tcg (3CG)](t.md#tcg)). {#list}

### Расчет метрики {#click-hyp-cg-calc}

Значение метрики равно сумме значений кликовых добавок результатов поисковой выдачи ($pclicks_{i}$), умноженных на $\frac{1}{1 + i}$:

$click{-}hyp{-}cg = \sum\limits_{i=0}^{n} \frac{pclicks_{i}}{1 + i}$
 
{% include [tcg-pclicks0](../_includes/concepts/t/id-tcg/pclicks0.md) %}


- основной: фактор ``WEB.FormulaValueDump_click``;
    
- альтернативный (если нет данных в основном): фактор `WEB_MISSPELL.FormulaValueDump_click`.
    

{% include [tcg-pclicks3](../_includes/concepts/t/id-tcg/pclicks3.md) %}


[К списку метрик](#list).


## cont {#cont}

Доля документов, содержащих порно-контент и нецензурную лексику, в первых n результатах поисковой выдачи.

### Расчет метрики {#cont-calc}

Значение метрики равно отношению количества документов, которым выставлены оценки <q>порно-контент</q> или <q>на грани</q>, к общему количеству документов (n):

$cont = \frac{n_{porn-cont}}{n} { ,}$
 
где
 $n_{porn-cont}$ — количество документов в первых десяти результатах поисковой выдачи, которым выставлена оценка <q>порно-контент</q> или <q>на грани</q>.

{% include [adv-judgeporn](../_includes/concepts/a/id-adv/judgeporn.md) %}


{% include [click-hyp-cg-backtolist](../_includes/concepts/c/id-click-hyp-cg/backtolist.md) %}


