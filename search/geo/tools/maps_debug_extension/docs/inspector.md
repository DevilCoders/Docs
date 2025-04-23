#Панель в веб инспекторе. Maps debug.
Содержит информацию по источникам запросов в верхний/нижний метапоиск, опечаточник итд.

##Файлы. 
Находятся в `js/inspector`.
`background.js` - При перезагрузке страницы отправляет сообщение что панель жука надо обновить.

Инициализация из файла manifest.json директива `"devtools_page": "inspector-output.html"`
Этот html файл встраивает `inspector-panel.html` в панель инструментов браузера. 
Состоит из подключения вспомогательных `table.js, input.js, cut.js` и основного `inspector-panel.js` скрипта.

###input.js
Обертка над стандартным браузерным инпутом. Создает инпут. Вешает нужный css класс

###cut.js
Создает элемент кат, ссылка-переключатель рядом с div-ом. Первым аргументов принимает строку, 
Все остальные - htmlElements которые будут спрятаны в скрывающийся блок.

###table.js
Создает таблицу. Принимает 2мерную матрицу, возвращает HtmlElement table таблицу.
``` 
 * var table = new Table([[a, 1], [b, 2]]);
 * table.render(document.body);
 *
 * -------------------------
 * | a        | 1          |
 * -------------------------
 * | b        | 2          |
 * -------------------------
 ```
 
 ###inspector-panel.js
 
 Точка входа - конструктор класса `Extension()` стр 48.
 - Здесь определяется есть ли серверные результаты поиска в ноде `.config-view`, если есть запускаем `_handleRequest()`
 для серверных результатов. 
 - Подписываемся на удачное завершение запроса браузера. `chrome.devtools.network.onRequestFinished.addListener`. 
 Фильтруем поисковые запросы по маске и запускаем тот же `_handleRequest()` метод

####_handleRequest()
Парсит и выводит поисковый JSON. Сначала берется ResponseMetaData - выводится. 

Далее ResponseMetaData.SearchResponse

далее ResponseMetaData.SearchResponse.InternalResponseInfo

далее ResponseMetaData.SearchResponse.InternalResponseInfo.debug

Если на каком-либо шаге данных нет, цепочка разбора JSON-a прерывается и выводится в html то что есть
в приватных переменных `this._templateRequests, this._allJson, this._factors`.


##Отладка
- Открыть панель разработчика в отдельном окне.
- Выбрать Maps Debug
- Нажать сочетание клавиш для вызова инспектора Cmd+Alt+J macos, и, кажется, F12 Windows.

Появится панель разработчика но для страницы панели Maps Debug.