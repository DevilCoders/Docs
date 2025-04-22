# A 

В данном разделе приведено описание метрик, первой буквой в названии которой является <q>A</q> (без учета [оцененности](naming.md#judged)). {#list}

## adv {#adv}

Доля документов, содержащих порно-рекламу в первых n результатах поисковой выдачи. {#list}

### Расчет метрики {#adv-calc}

Значение метрики равно отношению количества документов, которым выставлена оценка <q>порно-реклама</q>, к общему количеству документов (n):

$adv = \frac{n_{porn-adv}}{n} { ,}$
 
где
 $n_{porn-adv}$ — количество документов в первых n результатах поисковой выдачи, которым выставлена оценка <q>порно-реклама</q>.

Общие сведения об оценке так называемых <q>серых запросов</q> представлены в разделе [Оценка серых запросов](http://doc.yandex-team.ru/analytics/metrics/concepts/judgePorn.xml) документа [Оценка качества поиска](http://doc.yandex-team.ru/analytics/metrics/concepts/About.xml).

[К списку метрик](#list).


## authority-hyp-cg {#authority-hyp-cg}

Оценка поисковой выдачи на основе значения предсказанной авторитетности (компонента $authority_{i}$ метрики [tcg (3CG)](t.md#tcg))

### Расчет метрики {#authority-hyp-cg-calc}

Значение метрики равно сумме значений предсказанной авторитетности документов поисковой выдачи ($authority_{i}$), умноженных на $\frac{1}{1 + i}$:

$authority{-}hyp{-}cg = \sum\limits_{i=0}^{n} \frac{authority_{i}}{1 + i}$
 
{% include [tcg-authority0](../_includes/concepts/t/id-tcg/authority0.md) %}


- основной: фактор `WEB.FormulaValueDump__tw`;
    
- альтернативный (если нет данных в основном): фактор `WEB_MISSPELL.FormulaValueDump__tw`.
    

{% include [tcg-authority3](../_includes/concepts/t/id-tcg/authority3.md) %}


{% include [adv-backtolist](../_includes/concepts/a/id-adv/backtolist.md) %}



## averageQuerySpam {#averagequeryspam}

Доля запросов, ответы на которые содержат спам в первых n результатах поисковой выдачи.

### Расчет метрики {#averagequeryspam-calc}

Значение метрики равно отношению количества запросов, ответы на которые содержат по крайней мере один ответ, помеченный асессорами как спам ($n_{s}$), к общему количеству запросов ($n_{total}$):

$averageQuerySpam10 = \frac{n_{s}}{n_{total}}$
 
{% include [averagespam-markupspam](../_includes/concepts/a/id-averagespam/markupspam.md) %}


[К списку метрик](#list).


## averageSpam {#averagespam}

Доля спама в первых n результатах выдачи.

### Расчет метрики {#averagespam-calc}

Значение метрики равно отношению количества документов, отнесенных к одной из категорий спама, к общему числу документов (n):

$averageSpam = \frac{n_{s}}{n} { ,}$
 
где $n_{s}$ — количество документов в первых n результатах выдачи, отнесенных к одной из категорий спама.

Общие сведения об категориях спама представлены в разделе [Разметка спама](http://doc.yandex-team.ru/analytics/metrics/concepts/markupSpam.xml) документа [Оценка качества поиска](http://doc.yandex-team.ru/analytics/metrics/concepts/About.xml).

{% include [adv-backtolist](../_includes/concepts/a/id-adv/backtolist.md) %}


