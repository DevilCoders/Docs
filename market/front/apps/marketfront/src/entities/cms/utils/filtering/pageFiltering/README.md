# Функционал фильтрации cms страниц

## Зачем?
Есть продуктовые задачи, когда тот или иной лендинг нужно показать только определенной группе пользователей (плюсовикам, залогинам). Данные задачи решались различными изощереными способами: для ЧП 2020 был добавлен Маркер плюсовика, для проекта Мастеркард дополнительная страница с редиректом. Все это не давало общего решения данной продуктовой задачи, что приводило к дополнительной разработки на каждом конкретном проекте. Добавление фильтрации страниц предоставляет функционал для решения задач данного плана.

## Почему не доработали существующий функционал?
На данный момент есть определенный вид фильтрации страниц cms, который реализован с помощью Маркеров и Линков. Суть данного подхода заключается в том, что при запросе страницы фронт отправляет набор некоторых параметров и на основе этих параметров мы можем в cms конфигурировать условия скрытия страницы. При выполнении условия скрытия темплатор будет возвращать пустой результат. У данного подхода есть недостатки:
+ Параметры всегда вычисляются на фронте и отправляются в запрос в независимости от того используются ли они на данной странице или нет. Из-за этого асинхронное вычисление новых параметров может приводит к понижению производительности.ё
+ Отсутствие fallback логики, то есть когда пользователь не должен видеть страницу, мы не можем показать ему какой-либо кастомный контент объясняющий причину недоступности или сделать редирект на дефолтный лендинг.

## Как это работает?
В cms создан новый узел PAGE_HIDE_PARAMS, который добавлен для special страниц MP_PROMO_CONTEXT. При конфигурации данного узла, можно задать условия скрытия страницы, а так же fallback поведение при срабатывании данных условий. После загрузки cms странице на фронте, по параметрам скрытия страницы будут выполнены проверки условия скрытия, если параметров скрытия нет или условия не выполнены, страница будет отображена без изменений, иначе будет выполнено fallback поведение. Условия скрытия страницы совпадают с условиями скрытия виджета, при добавление нового условия оно прорастет сразу в двух местах.

## Fallback сценарии
+ Пользователь переходит на страницу, для него она должны быть скрыта, он видит коробку с надписью "Тут ничего нет". Аналогично тому, что увидит пользователь при скрытии через Маркер или Линки. Для получения данного поведения никаких дополнительных настроек кроме условий скрытия не нужно.
+ Пользователь переходит на страницу и видит контент, который объясняет ему почему для него эта страница недоступна. Для получения данного поведения необходимо сконфигурировать свойство "Содержимое" для "Условия скрытия страницы".
+ Пользователь переходит на страницу и происходит автоматический редирект на другую special cms страницу. Для получения данного поведения необходимо сконфигурировать свойство "Идентификатор страницы для редиректа" для "Условия скрытия страницы".

При выборе способа скрытия страницы, необходимо руководствоваться условием конкретной задачи, если функционала Линков и Маркеров хватает для решения задачи используйте их.
