# Архив

В разделе приведено описание офлайн-метрик, которые перестали использовать для оценки качества поиска. Причиной отказа послужило несоответствие затрат на поддержку метрик и эффективности их применения.

Архивные метрики сгруппированы по релизам документа, в рамках которых они были перенесены в данный раздел.

- [Релиз документа 3.0 от апреля 2016 г.](#release3-0)
- [Релиз документа 2.2 от сентября 2015 г.](#release2-2)


## Релиз документа 3.0 от апреля 2016 г. {#release3-0}

Метрики, перенесенные в архив: {#list1}

### ideal-spamDCG {#ideal-spamdcg}

Мера отклонения первых n результатов выдачи из-за спама с поправкой на [pfound](p.md#pfound) [идеального ответа](../reference/term.md#ideal-resp). Умножение усиливает вес спама для тех запросов, по которым идеальный ответ — хороший. 

#### Расчет метрики {#ideal-spamdcg}

Значение метрики рассчитывается по формуле:

$ideal{-}spamDCG = (\sum\limits_{i=1}^{n} conf(i) * \frac{1}{log_2(i+1)}) * pfound_{IA} { ,}$
 
где:

* $conf_{i}$ — вес $i$-го документа выдачи;
* $pfound_{IA}$ — [pfound](p.md#pfound) идеального ответа.

[К списку метрик](#list1).


### ideal-spam-pfound {#ideal-spam-pfound}

Общая оценка зарекламленности с поправкой на **pfound** [идеального ответа](../reference/term.md#ideal-resp).

Поправка на **pfound** идеального ответа позволяет усилить вес спама в тех выдачах, где идеальный ответ — хороший.

#### Расчет метрики {#ideal-spam-pfound}

Значение метрики рассчитывается по формуле:

$ideal{-}spam{-}pfound = spam{-}pfound * pfound_{ideal} { ,}$
 
где:

* $spam{-}pfound$ — общая оценка заспамленности выдачи;
* $pfound_{ideal}$ — **pfound** от идеального ответа.

{% include [ideal-spamdcg-backtolist1](../_includes/concepts/archive/id-ideal-spamdcg/backtolist1.md) %}



### normjudged-spamDCG {#normjudged-spamdcg}

Отклонение выдачи из-за спама с поправкой на оцененность.

Корректирует значение метрики [spamDCG](s.md#spamdcg) в зависимости от оцененности выдачи.

#### Расчет метрики {#normjudged-spamdcg}

Значение метрики равно отношению значений метрик [spamDCG](s.md#spamdcg) и [judged](j.md#judged):

$normjudged{-}spamDCG = \frac{spamDCG}{judged}$
 
{% include [ideal-spamdcg-backtolist1](../_includes/concepts/archive/id-ideal-spamdcg/backtolist1.md) %}



### normjudged-ideal-spamDCG {#normjudged-ideal-spamdcg}

Отклонение выдачи из-за спама с поправкой на pfound [идеального ответа](../reference/term.md#ideal-resp) и оцененность.

Корректирует значение метрики [ideal-spamDCG](#ideal-spamdcg) в зависимости от оцененности выдачи.

#### Расчет метрики {#normjudged-ideal-spamdcg}

Значение равно отношению значений метрик [ideal-spamDCG](#ideal-spamdcg) и [judged](j.md#judged):

$normjudged{-}ideal{-}spamDCG = \frac{ideal{-}spamDCG}{judged}$
 
{% include [ideal-spamdcg-backtolist1](../_includes/concepts/archive/id-ideal-spamdcg/backtolist1.md) %}



### p-N-adv {#p-n-adv}

Средняя оценка зарекламленности первых n результатов выдачи.

#### Расчет метрики {#p-n-adv}

Значение метрики равно отношению суммы выставленных потоку зарекламленности оценок к глубине выдачи ($n$):

$p{-}n{-}adv = \frac{\sum\limits_{i = 1}^{n} pRel_{ai}}{n} { ,}$
 
где
 $pRel_{ai}$ — вероятностный вес $i$-го элемента выдачи.

> ### Пример {#ex1}
> 
> Рассмотрим следующую выдачу:
> 
> $/left( /begin{array}{l} CLEAN// ANNOYING// BLOCKING// OK// CLEAN// CLEAN// BLOCKING// ANNOYING// BLOCKING// CLEAN /end{array} /right)$
> 
> С учетом вероятностных весов формула дает следующий результат:
> 
> $p{-}10{-}adv = \frac{0*4 + 1*0,1 + 2*0,2 + 3*0,5}{10} = 0,2$

{% include [ideal-spamdcg-backtolist1](../_includes/concepts/archive/id-ideal-spamdcg/backtolist1.md) %}



## Релиз документа 2.2 от сентября 2015 г. {#release2-2}

Метрики, перенесенные в архив: {#list}

* [judged-average-multi-pfound](#judged-average-multi-pfound)
* [multi-judged](#multi-judged)
* [multi-not-judged-query](#multi-not-judged-query)
* [multi-obj-present](#multi-obj-present)
* [multi-obj-present-rel](#multi-obj-present-rel)
* [multi-pfound](#multi-pfound)
* [spec-multi-pfound](#spec-multi-pfound)

### judged-average-multi-pfound {#judged-average-multi-pfound}

Среднее значение **pfound** для всех интентов запроса. В расчете учитываются только оцененные документы.

#### Расчет метрики {#judged-average-multi-pfound}

Значение метрики равно отношению суммы значение **pfound** для каждого интента к общему числу интентов:

$judged{-}average{-}multi{-}pfound = \frac{\sum\limits_{i=1}^{k+1} pfound(O_i)}{k+1} { ,}$
 
где:

* $O_1, O_2, ..., O_k, O_{k+1}$ — интенты запроса;
* $pfound(O_i)$ — pfound $i$-го интента;
* $O_{k+1}$ — интенты, не отнесенные ни к одной из категорий (<q>other</q>, другие).

{% include [multi-judged-backtolist](../_includes/concepts/archive/id-multi-judged/backtolist.md) %}



### multi-judged {#multi-judged}

Доля оцененных документов мультиобъектного поиска от суммарного количества документов на первой странице выдачи (с учетом результатов ранжирования и результатов колдунщиков).

#### Расчет метрики {#multi-judged}

Для расчета используется формула:

$multi{ }judged = \frac{n_{judged}}{n} {,}$
 
где:

* $n_{judged}$ — количество оцененных документов;
* $n$ — количество документов на первой странице выдачи с учетом результатов ранжирования и результатов колдунщиков.

[К списку метрик](#list).


### multi-not-judged-query {#multi-not-judged-query}

Доля неоцененных запросов, т. е. запросов, по которым отсутствуют оцененные документы.

#### Расчет метрики {#multi-not-judged-query}

Значение метрики равно отношению количества запросов, не имеющих ни одного оцененного документа, к общему количеству запросов:

$multi{-}not{-}judged{-}query = \frac{Q_{not judged}}{Q} { ,}$
 
где:

* $Q_{not judged}$ — количество запросов в группе, по которым отсутствуют оцененные документы в выдаче;
* $Q$ — суммарное количество запросов в группе.

{% include [multi-judged-backtolist](../_includes/concepts/archive/id-multi-judged/backtolist.md) %}



### multi-obj-present {#multi-obj-present}

Доля интентов, представленных в поисковой выдаче документами с оценками <q>R-</q> и выше. Из расчета исключается интенты, не отнесенные ни к одной из категорий (<q>other</q>).

#### Расчет метрики {#multi-obj-present}

Значение метрики равно отношению количества интентов, представленных оценками <q>R-</q> и выше, к общему количеству интентов (кроме <q>other</q>, другое):

$multi{-}obj{-}present = \frac{k_{rel-}}{k} { ,}$
 
где:

* $k_{rel-}$ — количество интентов (кроме <q>other</q>), представленных документами, имеющими оценки <q>R-</q> и выше;
* $k$ — количество интентов запроса (кроме <q>other</q>, другое).

{% include [multi-judged-backtolist](../_includes/concepts/archive/id-multi-judged/backtolist.md) %}



### multi-obj-present-rel {#multi-obj-present-rel}

Доля интентов, представленных в поисковой выдаче документами с оценками <q>R+</q> и выше. Из расчета исключается интенты, не отнесенные ни к одной из категорий (<q>other</q>).

#### Расчет метрики {#multi-obj-present-rel}

Значение метрики равно отношению количества интентов, представленных оценками <q>R+</q> и выше, и общего количества интентов (кроме <q>other</q>):

$multi{-}obj{-}present = \frac{k_{rel+}}{k} { ,}$
 
где:

* $k_{rel+}$ — количество интентов (кроме <q>other</q>), представленных документами, имеющими оценки <q>R+</q> и выше;
* $k$ — количество интентов запроса (кроме <q>other</q>, другое).

{% include [multi-judged-backtolist](../_includes/concepts/archive/id-multi-judged/backtolist.md) %}



### multi-pfound {#multi-pfound}

Суммарное значение **pfound** каждого интента с учетом веса данного интента в поисковой выдаче (взвешенный **pfound**).

#### Расчет метрики {#multi-pfound}

Значение метрики рассчитывается по формуле:

$multi{-}pfound = \sum_{i=1}^{k+1} w_i *pfound(O_i) { ,}$
 
где:

* $O_1, O_2, ..., O_k, O_{k+1}$ — интенты запроса;
* $O_{k+1}$ — интенты, не отнесенные ни к одной из категорий (<q>other</q>);
* $w_i$ — вес $i$-го интента;
* $pfound(O_i)$ — pfound $i$-го интента.

{% include [multi-judged-backtolist](../_includes/concepts/archive/id-multi-judged/backtolist.md) %}



### spec-multi-pfound {#spec-multi-pfound}

Взвешенный **pfound** для мультиобъектного поиска без учета интентов, не отнесенных к категориям (<q>other</q>).

#### Расчет метрики {#spec-multi-pfound}

Для расчета используется модифицированная формула метрики [multi-pfound](#multi-pfound):

$multi{-}pfound = \sum_{i=1}^{k} w_i *pfound(O_i) { ,}$
 
где:

* $O_1, O_2, ..., O_k$ — интенты запроса;
* $w_i$ — вес $i$-го интента;
* $pfound(O_i)$ — pfound $i$-го интента.

{% include [multi-judged-backtolist](../_includes/concepts/archive/id-multi-judged/backtolist.md) %}


