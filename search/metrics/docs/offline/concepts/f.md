# F

В данном разделе приведено описание метрик, первой буквой в названии которой является <q>F</q> (без учета [оцененности](naming.md#judged)). {#list}

## fastrobot {#fastrobot}

Доля документов, возвращенных из базы быстрого робота, в первых $n$ результатах поисковой выдачи.

### Расчет метрики {#fastrobot-calc}

Значение метрики равно отношению количества документов, возвращенных из базы быстрого робота, к общему количеству документов ($n$):

$fastrobot = \frac{n_{fast}}{n} { ,}$
 
где $n_{fast}$ — количество документов из базы быстрого робота в первых n результатах поисковой выдачи.

[К списку метрик](#list).


## fresh-video-judgedfresh {#fresh-video-judgedfresh}

Доля видеороликов, оцененных по шкале релевантности, среди свежих документов в первых пяти результатах поисковой выдачи.

### Расчет метрики {#fresh-video-judgedfresh-calc}

Значение метрики равно отношению количества документов, оцененных по шкале релевантности $n_{assessed}$ к общему числу документов поисковой выдачи с оценкой <q>Свежий</q> в первых пяти результатах. Если количество документов в выдаче с оценкой <q>Свежий</q> меньше пяти, то для расчета значения используется реальное количество документов.
 $fresh{-}video{-}judgedfresh = \frac{n_{assessed}}{min(n_{freshurls}, 5)}$
 
{% include [fastrobot-backtolist](../_includes/concepts/f/id-fastrobot/backtolist.md) %}

[Разметка свежести видео](https://ang2.yandex-team.ru/view/wiki?page=freshness_url) в `ang2.yandex-team.ru`

## fresh-video-p {#fresh-video-p}

Оценка релевантности и свежести контента первого видеоролика, дата создания которого не превышает трех суток (отображается при значении CGI-параметра <q>&within=8</q>).

### Расчет метрики {#fresh-video-p-calc}

Значение метрики равно вероятностному весу первого видеоролика, оцененного по шкале релевантности, с датой создания не превышающей трех суток (включительно).

Если документу выставлена оценка <q>Не свежий</q>, то значение метрики равно нулю.

При расчете метрики используются следующие условные вероятностные веса оцененных документов:

#|
|| **Типы оценки** | **Вероятностные веса 
для метрики fresh-video-fresh-p1** ||
|| Релевантный плюс (REL+) | 1 ||
|| Релевантный минус (REL-) | 0,5 ||
|| Нерелевантный (IRREAL) | 0,0 ||
|| SOFT_404 | 0,0 ||
|| 404 | 0,0 ||
|#

{% include [fastrobot-backtolist](../_includes/concepts/f/id-fastrobot/backtolist.md) %}

[Оценка релевантности видео](https://ang2.yandex-team.ru/view/wiki?page=videorel_russia#otsenkasostoyaniyarolika) в `ang2.yandex-team.ru`
[Разметка свежести видео](https://ang2.yandex-team.ru/view/wiki?page=freshness_url) в `ang2.yandex-team.ru`
[Метрика свежести видео](https://wiki.yandex-team.ru/video/VideoPoisk/Quality/Freshness/Metrics) в Вики

## fresh-video-queryfresh {#fresh-video-queryfresh}

Средняя оценка запроса по шкале свежести с поправкой на remap.

### Расчет метрики {#fresh-video-queryfresh-calc}

Метрика рассчитывается как произведение оценки свежести запроса, выставленной асессором, и коэффициента remap.
 $fresh{-}video{-}queryfresh = remap * freshintent { ,}$
 
где:

* $freshintent$ — значение интента свежести запроса;
* $remap$ — поправочный коэффициент.

При расчете метрики используются следующие значения интента свежести запроса и remap соответствующие оценке свежести запроса, выставленной асессором:

**Оценка асессора** | **freshintent** | **remap**
----- | ----- | -----
10 | 0 | 0
15 | 1 | 0,1
20 | 2 | 0,3
30 | 3 | 0,55
40 | 4 | 0,8


{% include [fastrobot-backtolist](../_includes/concepts/f/id-fastrobot/backtolist.md) %}

[Разметка свежести запросов](https://ang2.yandex-team.ru/wiki/-view?page=freshness_markup_rus) в `ang2.yandex-team.ru`
[Метрика свежести видео](https://wiki.yandex-team.ru/video/VideoPoisk/Quality/Freshness/Metrics) в Вики

## fresh-video-soft404-per-404 {#fresh-video-soft404-per-404}

Доля документов в первых пяти результатах выдачи по видеопоиску, имеющих оценку <q>404</q> или <q>soft404</q> и размеченных как свежие.

### Расчет метрики {#fresh-video-soft404-per-404-calc}

Значение метрики равно отношению количества документов, размеченных как свежие и имеющих оценку <q>404</q> или <q>soft404</q> к общему количеству документов, размеченных как свежие:

$fresh{-}video{-}soft404{-}per{-}404 = \frac{m_{404{, }soft404}}{n_{urlfresh}} { ,}$
 
где:

* $m_{404{, }soft404}$ — количество документов в пятерке, размеченных как свежие и имеющих оценку <q>404</q> или <q>soft404</q>;
* $n_{urlfresh}$ — количество документов в пятерке, размеченных как свежие.

{% include [fastrobot-backtolist](../_includes/concepts/f/id-fastrobot/backtolist.md) %}

[Разметка свежести видео](https://ang2.yandex-team.ru/view/wiki?page=freshness_url) в `ang2.yandex-team.ru`
[Оценка состояния ролика](https://ang2.yandex-team.ru/view/wiki?page=videorel_russia#otsenkasostoyaniyarolika) в `ang2.yandex-team.ru`
[Метрика свежести видео](https://wiki.yandex-team.ru/video/VideoPoisk/Quality/Freshness/Metrics) в Вики

## fresh-video-urlsfresh {#fresh-video-urlsfresh}

Доля видеороликов, размеченных как свежие, в первых пяти результатах выдачи.

### Расчет метрики {#fresh-video-urlsfresh-calc}

Значение метрики равно отношению количества документов, размеченных как свежие, к общему числу документов (5).

Если количество документов в выдаче меньше пяти, то для расчета значения используется реальное количество документов.
 $fresh{-}video{-}urlsfresh = \frac{n_{urlfresh}}{min(5, n_{urls})} { ,}$
 
где $n_{urlfresh}$ — количество документов в пятерке, размеченных как свежие.

{% include [fastrobot-backtolist](../_includes/concepts/f/id-fastrobot/backtolist.md) %}

[Разметка свежести видео](https://ang2.yandex-team.ru/view/wiki?page=freshness_url) в `ang2.yandex-team.ru`
[Метрика свежести видео](https://wiki.yandex-team.ru/video/VideoPoisk/Quality/Freshness/Metrics) в Вики

## fresh-video-wpfound {#fresh-video-wpfound}

Мера насыщения свежим видеоинтентом первой пятерки документов поисковой выдачи.

Показывает, какое количество свежего и несвежего интента нужно предоставить пользователю по запросу.

### Расчет метрики {#fresh-video-wpfound-calc}

Значение метрики равно сумме, слагаемыми которой являются:

- минимальное значение из количества свежего интента, которое предполагается показать пользователю, и показанного свежего интента;
- минимальное значение из количества интента, не являющегося свежим, которое предполагается показать пользователю, и показанного интента, не являющегося свежим.
 $fresh{-}video{-}wpfound = min(0.411 * queryfresh, fresh{-}pFound) + min(0.411 * (1 - queryfresh), nofresh{-}pFound) { ,}$
 
где:

* $queryfresh$ — оценка свежести запроса с поправкой на remap, показывающая какое количество свежего интента необходимо показать пользователю (значение метрики [fresh-video-queryfresh](#fresh-video-queryfresh));
* $fresh{-}pFound$ — значение метрики [pFound](p.md#pfound), при расчете которой учитываются только свежие документы из первой пятерки (несвежие документы выкидываются);
* $nofresh{-}pFound$ — значение метрики [pFound](p.md#pfound), при расчете которой учитываются только документы из первой пятерки не являющиеся свежими (свежие документы выкидываются);
* $0.411$ — коэффициент равный максимальному значению метрики [pFound](p.md#pFound) для первых пяти результатов выдачи с оценкой <q>REL+</q>.

{% include [fastrobot-backtolist](../_includes/concepts/f/id-fastrobot/backtolist.md) %}

[Метрика свежести видео](https://wiki.yandex-team.ru/video/VideoPoisk/Quality/Freshness/Metrics) в Вики
[Разметка свежести запросов](https://ang2.yandex-team.ru/wiki/-view?page=freshness_markup_rus) в `ang2.yandex-team.ru`

