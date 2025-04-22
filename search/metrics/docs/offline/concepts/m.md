# M

В данном разделе приведено описание метрик, первой буквой в названии которой является <q>M</q> (без учета [оцененности](naming.md#judged)). {#list}

## MAP {#map}

Близость расположения релевантных картинок к началу выдачи (метрика средней точности). 

Чем ближе релевантный документ к началу выдачи, тем больше его значимость для общей оценки.

{% note info %}

Учет близости релевантных документов к началу выдачи отличает метрику [MAP](#map) от метрики [p](p.md#p), которая игнорирует взаимное расположение элементов в первой десятке.

{% endnote %}


### Расчет метрики {#map-calc}

Пусть для данного запроса имеется $k$ релевантных документов. Точность $prec\_rel(i)$ на уровне $i$-го релевантного документа равна $precision(pos(i))$, если $i$-й релевантный документ находится в результатах запроса на позиции  $pos(i)$. Если $i$-й релевантный документ не найден, то  $prec\_rel(i) = 0$. Средняя точность для данного запроса равна среднему значению величины $prec\_rel(i)$ по всем $k$ релевантным документам:

$MAP = \frac{1}{k} \sum\limits_{i=1}^{k}prec\_rel(i)$
 
Доля релевантных документов $prec\_rel(i)$ среди $i$ первых элементов равна отношению количества релевантных элементов среди $i$ первых элементов к $i$:

$prec\_rel(i) = \frac{n_{r}(i)}{i} { ,}$
 
где $n_{r}$ — количество релевантных документов среди первых $i$ документов.

> ## Пример 1 {#ex1}
> 
> Рассмотрим две следующие выдачи:
> 
> $(1) { } /left( /begin{array}{l} R// R// IR /end{array} /right) { и (2)} { } /left( /begin{array}{l} R// IR// R /end{array} /right)$
> 
> По метрике **MAP** первая выдача будет оценена выше, чем вторая, т. к. в ней релевантные документы располагаются ближе к началу выдачи.
> 
> При этом наличие такого же количество релевантных элементов в первой выдаче (которая может быть сформирована из тех же документов) не влияет на расчет значения метрики. Важным для **MAP** является близость релевантных документов к началу выдачи. По метрике **p10** данные выдачи были бы оценены одинаково.

> ## Пример 2 {#ex2}
> 
> Зависимость оцененности выдачи по метрике **p10** и **MAP** отсутствует. Т. е. если выдача оценена выше другой по метрике **p10**, это не означает, что она будет оценена выше по метрике **MAP**.
> 
> Рассмотрим две следующие выдачи:
> 
> $(1) { } /left( /begin{array}{l} IR// IR// R// R// R /end{array} /right) { и (2)} { } /left( /begin{array}{l} R// R// IR// IR// IR /end{array} /right)$
> По метрике **MAP** выше будет оценена выдача (2), а по **p10** — (1).

{% include [mobile-access-hyp-cg-backtolist](../_includes/concepts/m/id-mobile-access-hyp-cg/backtolist.md) %}



## mobile-access-hyp-cg {#mobile-access-hyp-cg}

Компонента доступности документов поисковой выдачи на мобильном устройстве ( $mob/_access_{i}$ ) для метрики [mobile-tcg (m3CG)](#mobile-tcg).

### Расчет метрики {#mobile-access-hyp-cg-calc}

Значение метрики равно сумме значений фактора доступности документов поисковой выдачи на мобильном устройстве ($mob/_access_{i}$), умноженных на $\frac{1}{1 + i}$:

$mobile-access-hyp-cg = \sum\limits_{i=0}^{n} \frac{mob/_access_{i}}{1 + i}$
 
Информация о факторе доступности поступает из сервиса [Watto](https://wiki.yandex-team.ru/robot/watto/).

Возможные значения для $i$-го результата выдачи:

- <q>-1</q> — документ не доступен;
- <q>1</q> — документ доступен.

[К списку метрик](#list).


## mobile-authority-hyp-cg  {#mobile-authority-hyp-cg}

Компонента предсказанной авторитетности ($authority_{i}$) для метрики [mobile-tcg (m3CG)](#mobile-tcg).

### Расчет метрики {#mobile-authority-hyp-cg-calc}

Значение метрики равно сумме значений предсказанной авторитетности документов поисковой выдачи ($authority_{i}$), умноженных на $\frac{1}{1 + i}$:

$mobile-clicks-hyp-cg = \sum\limits_{i=0}^{n} \frac{authority_{i}}{1 + i}$
 
Значение предсказанной авторитетности вычисляется по формуле [66767](https://fml.yandex-team.ru/formula/66767) сервиса [fml](https://doc.yandex-team.ru/fml/overview/concepts/about.html). При отсутствии фактора, значение $authority_{i}=0$.

{% include [mobile-access-hyp-cg-backtolist](../_includes/concepts/m/id-mobile-access-hyp-cg/backtolist.md) %}



## mobile-clicks-hyp-cg  {#mobile-clicks-hyp-cg}

Кликовая добавка ($pclicks_{i}$) для метрики [mobile-tcg (m3CG)](#mobile-tcg).

### Расчет метрики {#mobile-clicks-hyp-cg-calc}

Значение метрики равно сумме значений кликовых добавок результатов поисковой выдачи ($pclicks_{i}$), умноженных на $\frac{1}{1 + i}$:

$mobile-clicks-hyp-cg = \sum\limits_{i=0}^{n} \frac{pclicks_{i}}{1 + i}$
 
Значение кликовой добавки вычисляется по формуле [64021](https://fml.yandex-team.ru/formula/64021) сервиса [fml](https://doc.yandex-team.ru/fml/overview/concepts/about.html). При отсутствии фактора, значение $pclicks_{i}=0$.

{% include [mobile-access-hyp-cg-backtolist](../_includes/concepts/m/id-mobile-access-hyp-cg/backtolist.md) %}



## mobile-remapped-hyp-cg {#mobile-remapped-hyp-cg}

Компонента релевантности ( $relevance_{i}$ ) для метрики [mobile-tcg (m3CG)](#mobile-tcg).

### Расчет метрики {#mobile-remapped-hyp-cg-calc}

Значение метрики равно сумме значений релевантности документов поисковой выдачи ($relevance_{i}$), умноженных на $\frac{1}{1 + i}$:

$mobile-remapped-hyp-cg = \sum\limits_{i=0}^{n} \frac{relevance_{i}}{1 + i}$
 
{% include [mobile-tcg-mobile-tcg-p-1](../_includes/concepts/m/id-mobile-tcg/mobile-tcg-p-1.md) %}


{% include [mobile-tcg-mobile-tcg-table](../_includes/concepts/m/id-mobile-tcg/mobile-tcg-table.md) %}


{% include [mobile-access-hyp-cg-backtolist](../_includes/concepts/m/id-mobile-access-hyp-cg/backtolist.md) %}



## mobile-tcg (m3CG) {#mobile-tcg}

Оценка ранжирования мобильного поиска на основе релевантности, кликовой добавки, предсказанной авторитетности и доступности документа на мобильном устройстве.

### Расчет метрики {#mobile-tcg-calc}

Метрика вычисляется по формуле:

$mobile-tcg = \sum\limits_{i=0}^{n} \frac{w_{r} * relevance_{i} + w_{ac} * mob/_access_{i} + w_{c} * pclicks_{i} + w_{au} * authority_{i}}{1 + i} { ,}$
 
где:

* $i$ — позиция документа в выдаче;
* $relevance_{i}$ — значение релевантности $i$-го результата выдачи (см. [таблицу](#mobile-tcg-p-1));
* $mob/_access_{i}$ — доступность $i$-го результата выдачи на мобильном устройстве. Возможные значения: <q>-1</q> — документ не доступен, <q>1</q> — документ доступен;
* $pclicks_{i}$ — значение кликовой добавки для $i$-ого результата выдачи. Вычисляется по формуле [64021](https://fml.yandex-team.ru/formula/64021) сервиса [fml](https://doc.yandex-team.ru/fml/overview/concepts/about.html). При отсутствии фактора, значение $pclicks_{i}=0$;
* $authority_{i}$ — предсказанная авторитетность для $i$-ого результата выдачи. Вычисляется по формуле [66767](https://fml.yandex-team.ru/formula/66767) сервиса [fml](https://doc.yandex-team.ru/fml/overview/concepts/about.html). При отсутствии фактора, значение $authority_{i}=0$;

При расчете метрики используются следующие значения релевантности оцененных документов: {#mobile-tcg-p-1}

**Типы оценки релевантности** | **Значение**
----- | -----
Витальный (V) | 1,0
Полезный (U) | 0,75
Релевантный плюс (R+) | 0,5
Релевантный минус (R-) | 0,25
Нерелевантный (IR) | 0,0


Значения весовых коэффициентов:

**Коэффициент** | **Значение**
----- | -----
$w_r$ | 0,49
$w_{ac}$ | 0,04
$w_{c}$ | 0,31
$w_{au}$ | 0,16


{% include [mobile-access-hyp-cg-backtolist](../_includes/concepts/m/id-mobile-access-hyp-cg/backtolist.md) %}

[Приемочная оффлайн метрика качества мобильного поиска m3cg (mobile 3cg)](https://old.wiki.yandex-team.ru/users/olycha/m3cgsummary) в Вики

## morda  {#morda}

Доля корневых страниц сайтов (<q>морд</q>), найденных в первых n результатах поисковой выдачи.

Пример корневой страницы сайта: [http://www.yandex.ru/](http://www.yandex.ru/)

Пример некорневой страницы сайта: [https://wiki.yandex-team.ru/TechDoc/ToolsMath](https://wiki.yandex-team.ru/TechDoc/ToolsMath).

### Расчет метрики {#morda-calc}

Значение метрики равно отношению количества корневых страниц к рассматриваемому числу документов выдачи (n).
 $morda = \frac{n_{root}}{n} { ,}$
 
где $n_{root}$ — количество корневых документов в первых n результатах поисковой выдачи.

{% include [mobile-access-hyp-cg-backtolist](../_includes/concepts/m/id-mobile-access-hyp-cg/backtolist.md) %}


