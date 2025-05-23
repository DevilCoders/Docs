# V

В данном разделе приведено описание метрик, первой буквой в названии которой является <q>V</q> (без учета [оцененности](naming.md#judged)). {#list}

## video-ndcg {#video-ndcg}

Мера отклонения выдачи видео от [идеального ответа](../reference/term.md#ideal-resp).

### Расчет метрики {#ndcg-calc}

Значение метрики **ndcg** равно отношению значения функции $dcg$ от первых n результатов выдачи системы к значению функции $dcg$ от идеального ответа для первых n результатов выдачи системы:

$(1) { } ndcg = \frac{dcg(sysAnswer)}{dcg(idealAnswer)} { ,}$
 
где:

* $sysAnswer$ — выдача системы;
* $idealAnswer$ — идеальная выдача.

Оценка идеального ответа производится с помощью функции $dcg$. Функция $dcg$ вычисляется по формуле:

$(2) { } dcg = \sum\limits_{i=1}^{n} conf(i) * \frac{1}{log_{2}(i+1)} { ,}$
 
где $conf(i)$ — вес $i$-го документа выдачи.

В формуле (2) суммируются веса первых n элементов выдачи с поправкой на удаленность релевантных элементов от ее начала. Данная поправка выполняется при помощи логарифмического отношения, которое понижает условный вес элементов, по мере их удаления от первой позиции выдачи. Информация о весах документов представлена в разделе [Условные вероятностные веса оцененных документов](http://doc.yandex-team.ru/analytics/metrics/reference/ElementsWeights.xml) документа [Оценка качества поиска](http://doc.yandex-team.ru/analytics/metrics/concepts/About.xml).

{% note info %}

Метрика **ndcg** принимает неопределенное значение (<q>undefined</q>), если значение функции $dcg$ от вектора идеального ответа равно нулю (если в идеальном ответе не содержится релевантных документов). Запрос, оцененный по метрике **ndcg** значением <q>undefined</q>, исключается из дальнейшего анализа.

{% endnote %}


### Корректировка условного веса элемента в зависимости от позиции в выдаче {#ndcg-correct}

Допустим, что витальный элемент (V) находится на первой позиции выдачи. Тогда в результате поправки его условный вес не изменится:

$ndcg(V_{1}) = 0,61 * \frac{1}{log_{2}(1+1)} = 0,61 { ,}$
 
где $V_{1}$ — витальный элемент на первой позиции выдачи.

Если витальный элемент находится на второй позиции, его условный вес уменьшится:

$ndcg(V_{2}) = 0,61 * \frac{1}{log_{2}(2+1)} /approx 0,385 { ,}$
 
где $V_{2}$ — витальный элемент на второй позиции выдачи.

Пример расчета метрики представлен в разделе [ndcg](n.md#ndcg).

{% include [vital-backtolist](../_includes/concepts/v/id-vital/backtolist.md) %}



## video-p-quality {#video-p-quality}

Средняя оценка видеоролика по шкале релевантности с поправкой на оценку по шкале качества (см. раздел [Оценка видео](http://doc.yandex-team.ru/analytics/metrics/concepts/judgeVideo.xml) документа [Оценка качества поиска](http://doc.yandex-team.ru/analytics/metrics/concepts/About.xml)). При расчете учитываются только те результаты выдачи, которые оценены по шкале качества.

### Расчет метрики {#video-p-quality-calc}

Значение равно отношению суммы произведений значений релевантности и качества видеоролика (см. приложение [Условные и вероятностные веса оцененных документов](http://doc.yandex-team.ru/analytics/metrics/reference/ElementsWeights.xml#video) документа [Оценка качества поиска](http://doc.yandex-team.ru/analytics/metrics/concepts/About.xml)) к количеству видеороликов, оцененных по шкале качества:

$video{-}p{-}quality = \frac{\sum\limits_{i=1}^{n} p_{i} * pq_{i}}{n} { ,}$
 
где:

* $p_{i}$ — оценка $i$-го видеоролика по шкале релевантности;
* $pq_{i}$ — вес оценки $i$-го видеоролика по шкале качества;
* $n$ — количество видеороликов, оцененных по шкале качества.

> ## Пример {#ex1}
> 
> Рассмотрим следующую выдачу:
> 
> $/left( /begin{array}{l} IR{, } HIGH// R+{, } LOW// R+{, } HIGH// R-{, } NORMAL// R+{, } NOT{ }JUDGED{ }ON{ }SCALE{ }QUALITY// R-{, } LOW// IR-{, } NORMAL// IR-{, } LOW// IR{, } NOT{ }JUDGED{ }ON{ }SCALE{ }QUALITY// R-{, } NOT{ }JUDGED{ }ON{ }SCALE{ }QUALITY /end{array} /right)$
> 
> Для данной выдачи $n=7$ и формула принимает вид:
> 
> $video{-}p{-}quality = \frac{0*1 + 1 * 0,8 + 1 * 1 + 0,5*0,9 + 0,5 * 0,8 + 0 * 0,9 + 0 * 0,8}{7} /approx 0,3786$

{% include [vital-backtolist](../_includes/concepts/v/id-vital/backtolist.md) %}



## video-quality {#video-quality}

Средняя оценка видеоролика по шкале качества (см. раздел [Оценка видео](http://doc.yandex-team.ru/analytics/metrics/concepts/judgeVideo.xml) документа [Оценка качества поиска](http://doc.yandex-team.ru/analytics/metrics/concepts/About.xml)). При расчете учитываются только те результаты выдачи, которые оценены по шкале качества.

### Расчет метрики {#video-quality-calc}

Значение равно отношению суммы весов оценок видеороликов, выставленных по по шкале качества, к общему количеству оцененных по данной шкале результатов:

$video{-}quality = \frac{\sum\limits_{i=1}^{n} pq_{i}}{n} { ,}$
 
где:

* $pq_{i}$ — вес оценки $i$-го видеоролика по шкале качества;
* $n$ — количество видеороликов, оцененных по шкале качества.

Сведения о весах оценок качества видео представлены в приложении [Условные и вероятностные веса оцененных документов](http://doc.yandex-team.ru/analytics/metrics/reference/ElementsWeights.xml#video) документа [Оценка качества поиска](http://doc.yandex-team.ru/analytics/metrics/concepts/About.xml).

{% include [vital-backtolist](../_includes/concepts/v/id-vital/backtolist.md) %}



## vital {#vital}

Позиция витального документа среди первых n результатов выдачи.

Метрика вычисляется для запросов, в результатах поиска по которым присутствуют витальные документы.

Если по запросу находится более одного витального документа для расчета значения метрики используется только один из них, расположенный наиболее близко к первой позиции выдачи.

### Расчет метрики {#vital-calc}

Значение метрики рассчитывается по формуле:

$vital = /left/{ /begin{array}{ll} 1 - \frac{n_{vit}}{n} {,} & n_{vit} < n// 0 {,}& n_{vit} /geq n /end{array} /right. { ,}$

где:

* $n_{vit}$ — номер позиции витального документа;
* $n$ — рассматриваемая глубина поисковой выдачи.

Позиция считается с нуля, т. е. для витального документа на первой позиции $n_{vit}=0$, на второй — $n_{vit}=1$ и т. д.

[К списку метрик](#list).

