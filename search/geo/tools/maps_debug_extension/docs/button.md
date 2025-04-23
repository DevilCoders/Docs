# Кнопка жука на странице карт. Ламопчки в поисковом списке.

![uml](https://a.yandex-team.ru/api/v2/repos/arc/downloads?at=trunk&path=%2Fsearch%2Fgeo%2Ftools%2Fmaps_debug_extension%2Fdocs%2Fbutton-arch.png)

### Файлы.
`js/content/`
Диалоги кнопки собраны в `js/content/dialogs/`

`background.js` - слушает сетевые запросы, поисковый запрос редиректит с параметрами жука.

Точка входа - `js/content/init.js`

Для удобства подключения файлов используется модульная система [ymodules](https://github.com/ymaps/modules).

#### init.js
Ждет пока загрузится страница. Потом ждет еще 300мс. (Контент может перерисоваться из клиентского js)
и запускает конструктор `MapsService()`

#### maps-service.js
Добавляет кнопку жука на [страницу](https://github.yandex-team.ru/maps/maps-debug-extension/blob/master/js/content/maps-service.js#L30). 

Подписывается на все сетевые запросы `_requestHook()`. Для поисковых строит лампочки и диалоги `_buildDialogsAndBulbs()`.

[Подписывается](https://github.yandex-team.ru/maps/maps-debug-extension/blob/master/js/content/maps-service.js#L41) на изменение вертикали от диалога запускает `_changeVertical()`
 
Создает новый экземпляр `SearchRequest()` и `SuggestRequest()`

Если есть серверные результаты поиска в ноде `[data-block=config-view]` (она сохранена в конфиге)
то запускает по ним `_buildDialogsAndBulbs()`.

#### search-request.js
Получает и парсит поисковый результат.

#### suggest-request.js
Получает и парсит саджестовый результат (почти то же, что и в `search-request.js`).

#### bulbs.js
Прокси для добавления лампочек на страницу. 
Для каждой поисковой карточки запускается конструктор `Bulb()`

#### bulb.js
Все что скрывается за кликом на лампочку.
Получает в конструкторе url, sidebar (для встраивания), источники (для запроса за подсветкой).

Основная функциональность. По клику находим айди организации или объекта ЕК. И строим контент попапа
соответсвенно айди `_generateBusinessPopup()`. Запросы к бекенду осуществлюят
методы `getTarcHighlighted()` и `getFactors()`.

Методы `makeHightlight(), parseNames(), parseOrg(), getTarcHighlighted()` не изменились.

#### qtree.js
Файл не изменился. Завернут в модульную обертку. Метод `getDomNode()` возвращает сгенеренную ноду. 

#### url.js
Утилита для построения и парсинга урлов.

### Диалоги.
`js/content/dialogs`

#### Факторы. 
`js/content/dialogs/factors.js`
Если есть источник формирует ссылку подставляя хост и порт источника. 
Таким образом, если источник не определен то ссылки на факторы нет.

#### Запрос.
`js/content/dialogs/request.js`
На основе поисковых данных `internalResponseInfo` (или `this._data`) из `search-request.js` генерирует окно с 
деревом запросов и информацией по нему. 

Генерация происходит в методе `_infoBar()`

Поля `What, Where, ToponymProbability итд` перенесены из жука первой версии. 
Тут же (в `_infoBar()`) на основе данных поля `primary_source` 
создает дерево запросов создавая экземпляр `new QTree()`.

Методы `_createSourceInfo()`, `_filterSourceUrl()`, `_createQLossField()`, `_calcQloss()`,` _calcQlossHandler()`, `_replaceHostToStable()` остались без изменений.

#### Вертикали.
`js/content/dialogs/verticals.js`
На основе данных запроса `this._data` формирует список вертикалей.
Список генерируется в `_mainVerticalSelector()`
При выборе вертикали кидает событие `change-vertical` которое в итоги слушает `MapsService()`.

#### Саджест.
`js/content/dialogs/suggest.js`
На основе поисковых данных из `suggest-request.js` генерирует окно с информацией по саджесту и кулоссом. 

Генерация происходит в методе `_infoBar()`

#### Настройки.
`js/content/dialogs/settings.js`
Генерит ссылку на поле из конфига `helpPageUrl`
 
### Что нужно чтобы добавить урл котором должен работать экстеншн?
- Добавить урл в `manifest.json` в директивы `matches` и `permissions`
- Добавить урл в массив `mapsUrls` в файле `background.js`
