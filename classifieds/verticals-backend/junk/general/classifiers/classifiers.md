# Классификаторы Я.Объявлений

## "Классификатор для фидов"

API: `g-title-classifier-api`

Обучение: 
  - [граф в нирване](https://nirvana.yandex-team.ru/flow/01e628a6-dbe4-48f9-887c-ff50c7de23f7/647e6cf4-3966-4232-9896-4a297a8bb6d7/graph)
  - [таска в реакторе](https://nirvana.yandex-team.ru/browse?selected=9019487)

Определяет категорию товара по заголовку и хинту (любая, в том числе и не листовая категория).
Выдает только конечные категории.

Используется для определения категории фидовых объявлений.

### Данные для обучения

1. РУЧНЫЕ офферы, которые прошли проверку через clean-web (используются логи Модерации)
2. Переносы (перекладывания) РУЧНЫХ офферов из одной категории в другую
3. Хинты сгенерированы случайным образом - 
   66% - ожидаемая категория
   11% - без хинта
   11% - случайная категория
   12% - категории полученные из маппинга авито: получаем все категории авито ссылающиеся на ожидаемую, 
         по ним находим все категории нашего каталога
   
Категории со слишком маленьким числом примеров отбрасываются

### Принцип работы

Модель имеет два входа - для тайтлов и хинтов, оба входа ожидают строку, можно передать несколько категорий
через разделитель ';'

Далее вход тайтлов обрабатывается предобученной моделью `distilbert-base-multilingual-cased`
https://huggingface.co/distilbert-base-multilingual-cased

Входные категории кодируются в one_hot и складываются, не-конечные категории выражаются как сумма всех потомков

Полученные эмбеддинги конкатенируются, сверху устанавливается несколько полносвязных слоёв

Итоговая модель выдает вероятности принадлежности тайтла к каждой категории (сумма вероятностей равна 1).

Итоговая модель + маппинг из выходов модели в классы + один пример для "прогрева" модели при запуске
архивируются, архив записывается в S3.

## "Классификатор для формы добавления"

API: `g-title-suggest-api`

Обучение: [граф в Нирване](https://nirvana.yandex-team.ru/flow/e87cce0b-a661-4c2d-a2dd-9c66d8fb8762/c433b1b4-62b4-40eb-bed7-2a50d49ab50e/graph)

[Реакция](https://reactor.yandex-team.ru/browse?selected=8431727) в Ректоре, клонирующая и запускающая граф в Нирване.

Какие-то метрики обучения добавляются в [Пульсар](https://nda.ya.ru/t/hGfRQTS73nRyqL) с тегом `general-add-form-classifier`

Определяет категорию товара по заголовку.
Выдает конечные и неконечные категории.

Используется для определения категории на форме добавления.

### Данные для обучения

1. Синонимы категории из каталога (из поля `synonyms`)
2. РУЧНЫЕ офферы, которые прошли проверку через clean-web (используются логи Модерации)
3. Переносы (перекладывания) РУЧНЫХ офферов из одной категории в другую

Если в конечной категории А много примеров, то эти примеры используются для обучения классификации категории A.
Примеры для категорий, в которых примеров мало, используются для обучения классификации родительской категории.
То есть, если в категории мало примеров, то вместо этой категории классификатор будет предсказывать ее родителя.

Если же после "переноса" примеров на один уровень вверх все равно остаются категории с маленьким числом примеров, то
эти категории и примеры вообще не участвуют в обучении.

### Принцип работы

Над предобученной моделью устанавливается нескольких полносвязных слоев,
получившийся классификатор обучается с маленьким learning-rate.
В качестве предобученной модели используется `distilbert-base-multilingual-cased`:
https://huggingface.co/distilbert-base-multilingual-cased

Итоговая модель выдает вероятности принадлежности тайтла к каждой категории (сумма вероятностей равна 1).

Итоговая модель + маппинг из выходов модели в классы + один пример для "прогрева" модели при запуске
архивируются, архив записывается в S3.

## "Классификатор запросов"

API: `g-query-classifier-api`

Обучение: нет

Определяет категорию, в которой находятся товары, подходящие под поисковый запрос.
Выдает конечные и неконечные категории.

Используется для бустинга категорий в поиске.

### Данные для изначального обучения

1. Разметка самых популярных запросов по категориям в Толоке: https://st.yandex-team.ru/CLASSBACK-995
2. Небольшое количество тайтлов офферов, поданных с формы добавления
3. Небольшое количество перекладываний РУЧНЫХ офферов из одной категории в другую

Тайтлы офферов нужны для того, чтобы покрыть редкие категории, которые не попали в разметку в Толоке.
Используются только тайтлы только ручных офферов, так как в этих данных них меньше шума
(категория валидируется человеком, подающим объявление).

Граф с обучением модели: [ссылка](https://nirvana.yandex-team.ru/flow/dca1a931-76ac-4cb8-bdf9-fa4749b17568/5e5a5a67-a58d-40b6-ab18-4d1e84bf016a/graph/FlowchartBlockOperation/f4c9cc80-6722-4e99-84ce-8f322e2024a3)

### Принцип работы

Над предобученной моделью устанавливается нескольких полносвязных слоев,
получившийся классификатор обучается с маленьким learning-rate.
В качестве предобученной модели используется `distilbert-base-multilingual-cased`:
https://huggingface.co/distilbert-base-multilingual-cased

Итоговая модель выдает вероятности принадлежности запроса к каждой категории, которая была в обучении (сумма вероятностей равна 1).
