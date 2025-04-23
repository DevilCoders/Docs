# J

В данном разделе приведено описание метрик, первой буквой в названии которой является <q>J</q>. {#list}

## judged {#judged}

Доля оцененных документов в первых n результатах поисковой выдачи. 

### Расчет метрики {#judged-calc}

Значение метрики равно отношению количества оцененных документов $n_{assessed}$ к общему числу документов выдачи. Если количество документов в выдаче меньше n, то для расчета значения используется реальное количество документов.

$judged = \frac{n_{assessed}}{min(n_{urls}, n)}$
 
Для пустого SERP значение метрики равно единице.

[К списку метрик](#list).


## judged-age {#judged-age}

Свежесть оценок документов SERP. Рассчитывается средний возраст оценок документов по шкале релевантности по отношению к возрасту SERP.

### Расчет метрики {#judged-age-calc}

Разница в датах скачивания SERP и оценки документов считается в днях. Округление выполняется в меньшую сторону.

Значение метрики вычисляется по формуле:

$judged{-}age = \frac{\sum\limits_{i=1}^{n} serp - date_i}{n} { ,}$
 
где:

* $serp$ — дата и время скачивания SERP;
* $date_{i}$ — дата и время оценки $i$-го документа по шкале релевантности;
* $n$ — рассматриваемой количество документов в выдаче.

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-authority {#judged-authority}

Доля документов поисковой выдачи, для которых известно значение предсказанной авторитетности.

### Расчет метрики {#judged-authority-calc}

Значение метрики равно отношению количества документов, по которым известна предсказанная авторитетность ($n_{authority}$), к общему числу документов ($n$):

$judged{-}authority = \frac{n_{authority}}{n}$
 
Информация о предсказанной авторитетности поступает из массива `SearcherProp`. Источники:

- основной: фактор `WEB.FormulaValueDump__tw`;
    
- альтернативный (если нет данных в основном): фактор `WEB_MISSPELL.FormulaValueDump__tw`.
    

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-average-position {#judged-average-position}

Средняя позиция оцененных документов.

### Расчет метрики {#judged-average-position-calc}

Значение метрики равно отношению сумм позиций оцененных документов к количеству оцененных документов:

$judged{-}average{-}position = \frac{\sum\limits_{i=1}^{n} p_i}{n} { ,}$
 
где:

* $p_{i}$ — позиция $i$-го оцененного документа;
* $n$ — количество оцененных документов.

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-click {#judged-click}

Доля документов поисковой выдачи, для которых известно значение кликовой добавки.

### Расчет метрики {#judged-click-calc}

Значение метрики равно отношению количества документов, по которым известно значение кликовой добавки ($n_{click}$), к общему числу документов ($n$):

$judged{-}click = \frac{n_{click}}{n}$
 
Информация о кликовой добавке поступает из массива `SearcherProp` (фактор `WEB.FormulaValueDump_click`).

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-duplicate-images-p {#judged-duplicate-images-p}

Средняя оценка релевантности картинок со штрафом за наличие дубликатов в первых n результатах поисковой выдачи.

### Расчет метрики {#judged-duplicate-images-p10-calc}

Значение метрики рассчитывается по формуле:

$judged{-}duplicate{-}images{-}p = \frac{\sum\limits_{i=1}^{n} 0,5^{DupsBefore_i} BaseRel_i}{n} { ,}$
 
где:

* $DupsBefore_i$ — количество дубликатов картинки ($i)$, расположенных выше нее в поисковой выдаче;
* $BaseRel_i$ — оценка релевантности картинки (cм. приложение [Условные и вероятностные веса оцененных документов](https://doc.yandex-team.ru/analytics/metrics/reference/ElementsWeights.xml#imagesweights) документа [Оценка качества поиска](https://doc.yandex-team.ru/analytics/metrics/concepts/About.xml)).
* $n$ — общее число документов в выдаче.

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-language {#judged-language}

Доля документов с оценкой языка, полученной хотя бы из одного источника (SERP, KiWi, Толока), в первых n результатах поисковой выдачи.

### Расчет метрики {#judged-language-calc}

Значение метрики равно отношению количества документов, для которых получена оценка языка как минимум из одного источника: SERP, KiWi, Толока, к общему количеству документов (`n`).
 $judged{-}language = \frac{n_{language}}{n} { ,}$
 
где $n_{language}$ — количество документов в первых n результатах поисковой выдачи, для которых есть данные по языку.

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-language-kiwi {#judged-language-kiwi}

Доля документов с оценкой языка, полученной из KiWi, в первых n результатах поисковой выдачи.

### Расчет метрики {#judged-language-kiwi-calc}

Значение метрики равно отношению количества документов, для которых получена оценка языка из KiWi, к общему количеству документов (`n`):

$judged{-}language{-}kiwi = \frac{n_{language-kiwi}}{n} { ,}$
 
где $n_{language-kiwi}$ — количество документов в первых `n` результатах поисковой выдачи, для которых получена оценка языка из Kiwi.

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-language-toloka {#judged-language-toloka}

Доля документов с оценкой языка, полученной из [Толоки](https://doc.yandex-team.ru/analytics/toloka-guide/concepts/about.xml), в первых n результатах поисковой выдачи.

### Расчет метрики {#judged-language-toloka-calc}

Значение метрики равно отношению количества документов, для которых получена оценка языка из Толоки, к общему количеству документов (`n`):

$judged{-}language{-}toloka = \frac{n_{language-toloka}}{n} { ,}$
 
где $n_{language-toloka}$ — количество документов в первых `N` результатах поисковой выдачи, которым выставлена оценка языка в Толоке.

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-mobile-access {#judged-mobile-access}

Доля документов, для которых известно значение фактора доступности на мобильном устройстве.

### Расчет метрики {#judged-mobile-access-calc}

Значение метрики равно отношению количества документов, по которым известно значение фактора доступности ($n_{mobile{-}access}$), к общему числу документов мобильной выдачи ($n$):

$judged{-}mobile{-}access = \frac{n_{mobile{-}access}}{n}$
 
Информация о факторе доступности поступает из сервиса [Watto](https://wiki.yandex-team.ru/robot/watto/).

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-mobile-authority {#judged-mobile-authority}

Доля документов мобильной поисковой выдачи, для которых известно значение предсказанной авторитетности.

### Расчет метрики {#judged-mobile-authority-calc}

Значение метрики равно отношению количества документов, по которым известна предсказанная авторитетность ($n_{mobile{-}authority}$), к общему числу документов ($n$):

$judged{-}mobile{-}authority = \frac{n_{mobile{-}authority}}{n}$
 
Информация о предсказанной авторитетности поступает из сервиса [fml](https://doc.yandex-team.ru/fml/overview/concepts/about.html) (формула [66767](https://fml.yandex-team.ru/formula/66767)).

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-mobile-click {#judged-mobile-click}

Доля документов мобильной поисковой выдачи, для которых известно значение кликовой добавки.

### Расчет метрики {#judged-mobile-click}

Значение метрики равно отношению количества документов, по которым известно значение кликовой добавки ($n_{mobile{-}click}$), к общему числу документов ($n$):

$judged{-}mobile{-}click = \frac{n_{mobile{-}click}}{n}$
 
Информация о кликовой добавке поступает из сервиса [fml](https://doc.yandex-team.ru/fml/overview/concepts/about.html) (формула [64021](https://fml.yandex-team.ru/formula/64021)).

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judgedN-duplicate-images {#judgedn-duplicate-images}

Доля картинок, оцененных на наличие дублей, в первых n результатах поисковой выдачи.

### Расчет метрики {#judgedn-duplicate-images}

Значение метрики равно отношению количества оцененных документов $n_{assessed}$ к общему числу документов ($n$). Если количество документов в выдаче меньше $n$, то для расчета значения используется реальное число документов ($n_{urls}$).
 $judgedN{-}duplicate{-}images = \frac{n_{assessed}}{min(n_{urls}, n)}$
 
{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-normalized-duplicate-images-p {#judged-normalized-duplicate-images-p}

Скорректированное значение средней оценки релевантности картинок со штрафом за наличие дубликатов в первых n результатах поисковой выдачи.

### Расчет метрики {#judged-duplicate-images-p10-calc_1}

Значение метрики рассчитывается по формуле:

$judged{-}normalized{-}duplicate{-}images{-}p = \frac{\sum\limits_{i=1}^{n} 0,5^{DupsBefore_i} BaseRel_i}{min(n_{urls}, )} { ,}$
 
где:

* $DupsBefore_i$ — количество дубликатов картинки ($i)$, расположенных выше нее в поисковой выдаче;
* $BaseRel_i$ — оценка релевантности картинки (cм. приложение [Условные и вероятностные веса оцененных документов](https://doc.yandex-team.ru/analytics/metrics/reference/ElementsWeights.xml#imagesweights) документа [Оценка качества поиска](https://doc.yandex-team.ru/analytics/metrics/concepts/About.xml)).
* $n$ — общее число документов в выдаче ($n$). Если количество документов в выдаче меньше $n$, то для расчета значения используется реальное число документов ($n_{urls}$).

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}



## judged-queries {#judged-queries}

Доля запросов, по которым выставлены оценки асессоров.

### Расчет метрики {#judged-queries-calc}

Значение метрики равно отношению количества запросов, по которым выставлена по крайней мере одна оценка асессоров, к общему количеству скаченных запросов:

$judged{-}queries = \frac{n_{judged-queries}}{TQ} { ,}$
 
где:

* $n_{judged−queries}$ — количество оцененных запросов;
* $TQ$ — общее количество скаченных запросов, для которых выполняется усреднение.

{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}

Раздел [Общая схема оценки качества Поиска](http://doc.yandex-team.ru/analytics/metrics/concepts/generalDevelScheme.xml) документа [Оценка качества поиска](http://doc.yandex-team.ru/analytics/metrics/concepts/About.xml)

## judged-tw {#judged-tw}

Доля документов поисковой выдачи, оцененных по шкале асессорской авторитетности ([шкала доверия TRUSTWORTHINESS](https://wiki.yandex-team.ru/trustworthiness#shkalaocenki)).

### Расчет метрики {#judged-tw}

Значение метрики равно отношению количества документов, оцененных по шкале асессорской авторитетности ($n_{tw}$), к общему числу документов ($n$):

$judged{-}tw = \frac{n_{tw}}{n}$
 
{% include [judged-backtolist](../_includes/concepts/j/id-judged/backtolist.md) %}


