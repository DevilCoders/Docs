# Селекторница

### Что это?
Селекторница - это инструмент для поиска селекторов для автотестов.

Скрыта в боковой панели страниц под буквой "S":  
<img src="https://jing.yandex-team.ru/files/dariaborisyak/uhura_2021-02-17T14%3A25%3A41.906092.jpg" height="200px"/>
<img src="https://jing.yandex-team.ru/files/dariaborisyak/uhura_2021-02-17T14%3A17%3A58.137440.jpg" height="200px"/>

При клике на букву "S" в правом нижнем углу появляется панель для поиска селекторов:  
<img src="https://jing.yandex-team.ru/files/dariaborisyak/uhura_2021-02-17T14%3A28%3A51.073493.jpg" height="200px" />

Также панель появится, если добавить к урлу страницы параметр `_show_selectors=true`.

Кнопка "Получить хэш-таблицу" запускает подсчет data-хэшей для компонентов:  
<img src="https://jing.yandex-team.ru/files/dariaborisyak/uhura_2021-02-17T14%3A31%3A15.145028.jpg" height="200px" />

 После того, как хэши получены, можно получить селекторы с компонентами, кликнув на любой элемент страницы:  
 <img src="https://jing.yandex-team.ru/files/dariaborisyak/uhura_2021-02-17T14%3A17%3A59.265042.jpg" height="400px" />
 
Если не посчитать хэши, по клику на элемент будут выдаваться только селекторы без компонентов (но с data-e2e, танкерными ключами и, если больше ничего не нашлось, с тегами).

Корректность селектора можно проверить в консоли браузера:
<img src="https://jing.yandex-team.ru/files/dariaborisyak/uhura_2021-02-17T14%3A36%3A44.337314.jpg" height="400px" /> 

### Как это работает

Таблица с data-хэшами высчитывается в резолвере <a href="https://github.yandex-team.ru/market/partnernode/blob/01846d1fbd00c3780b9e8c7294aec63123ef9d11/shared/resolvers/hashSelectors/getFreshHashTable.js">getFreshHashTable</a>.

Полученная таблица записывается в localStorage под именем `HASH_TABLE`.

Уникальный селектор находится при помощи рекурсивной функции <a href="https://github.yandex-team.ru/market/partnernode/blob/01846d1fbd00c3780b9e8c7294aec63123ef9d11/client.next/containers/Page/AutotestSelectorFinder/utils.js#L161-L271">getSelector</a>.  
Приоритет атрибутов, по которым строится селектор:
- data-e2e
- танкерный ключ
- data-tid (React-компонент)
- css-класс (только из <a href="https://github.yandex-team.ru/market/partnernode/blob/01846d1fbd00c3780b9e8c7294aec63123ef9d11/client.next/containers/Page/AutotestSelectorFinder/constants.js#L12">white-листа</a>)
- тег (исключаются теги из <a href="https://github.yandex-team.ru/market/partnernode/blob/01846d1fbd00c3780b9e8c7294aec63123ef9d11/client.next/containers/Page/AutotestSelectorFinder/constants.js#L9">black-листа<a>)

Таким образом, если у элемента есть, например, и data-e2e, и data-tid, то в селектор попадет только data-e2e.

На каждом шаге селектор проверяется на уникальность. Если он не уникальный - поднимаемся на ноду выше.

### Проблемы и дальнейшие шаги

1. **В таблице с data-хешами отсутствуют компоненты из Левитана.**

Происходит это потому, что в ПИ они поступают в уже собранном, обработанном реселектором виде, и содержат такой комментарий:

`/*__reselector__start__::{"ComponentName":{"data-tid":"c21d6142"}}::__reselector__end__*/`.  

При повторной обработке реселектором файлы с таким комментарием игнорируются функцией <a href="https://github.yandex-team.ru/market/partnernode/blob/01846d1fbd00c3780b9e8c7294aec63123ef9d11/shared/resolvers/hashSelectors/getFreshHashTable.js#L46">setHash</a>, и в таблицу не попадают.

После того, как в реселектор будет вмёржен <a href="https://github.com/lttb/reselector/pull/91">пулл-реквест с фиксом</a>, нужно будет поднять версию реселектора в Левитане и в partnernode. Это даст возможность получать селекторы с компонентами из Левитана.

Тикет: <a href="https://st.yandex-team.ru/MARKETPARTNER-23221">MARKETPARTNER-23221</a>

2. **Получать хеши из <a href="https://pages.github.yandex-team.ru/market/partnernode/reselector/">Reselector Hash Table</a>**

Если страница открывается в БТ, то нет необходимости считать data-хеши с нуля - можно просто взять данные из <a href="https://pages.github.yandex-team.ru/market/partnernode/reselector/">Reselector Hash Table</a>.
Для этих целей готов резолвер <a href="https://github.yandex-team.ru/market/partnernode/blob/01846d1fbd00c3780b9e8c7294aec63123ef9d11/shared/resolvers/hashSelectors/getMasterHashTable.js">getMasterHashTable</a>, но его не пускает в гитхаб - вместо таблицы он видит 404.

Нужно разобраться с настройкой прав.

Тикет: <a href="https://st.yandex-team.ru/MARKETPARTNER-24117">MARKETPARTNER-24117</a>

3. **На демостендах не работает подсчет data-хешей**

Если открыть селекторницу на демостенде, не удается запустить вычисление data-хешей для компонентов. В консоли видна ошибка:

`REMOTE_RESOLVER_ERROR; ValidationError: Resolver hashSelectors/getFreshHashTable:getFreshHashTable is not found`

Методом точечного комментирования кода была обнаружено, что проблема кроется в импортах `fast-glob` и `@babel/core`.
Нужно разобраться, что с ними не так.

Тем временем, на логрусах всё работает правильно.

Тикет: <a href="https://st.yandex-team.ru/MARKETPARTNER-23527">MARKETPARTNER-23527</a>
