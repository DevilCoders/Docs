## Карты различных активностей на странице

### Конструкторы

* `MetrikaInpage.ClickMap` -- карта кликов
* `MetrikaInpage.ScrollMap` -- карта скролов
* `MetrikaInpage.LinkMap` -- карта ссылок

### Общие для всех карт параметры

    /**
     * @type Node/String
     * Элемент, куда отрендерить виджет.
     */
    renderTo: null,

    /**
     * @type String
     * CSS-класс корневого элемента.
     */
    className: '',

    /**
     * Счётчик, у которого смотрим статистику.
     * @type Number
     */
    counterId: 0,

    /**
     * Адрес страницы, с которой начнём просмотр.
     * @type String
     */
    url: '',

    /**
     * Режим карты. Может быть normal (обычная карта) или comparison (сравнение сегментов).
     * @type String
     */
    mode: 'normal',

    /**
     * Начальная и конечная даты периода, за который смотрим статистику. Массив из двух элементов со строками в формате Y-m-d.
     * @type Array
     */
    period: [],

    /**
     * Фильтр сегментации.
     * @type String
     */
    filter: '',

    /**
     * Размер виджета. Массив вида [width, height].
     * @type Array
     */
    size: [500, 500],

### Общие для всех карт методы

    /**
     * Изменяет размер виджета.
     *
     * @param {Array} size Массив вида [width, height].
     */
    setSize: function(size) {

    /**
     * Загружает страницу, на которой будем смотреть карты.
     *
     * @param {String} url
     */
    setUrl: function(url) {

    /**
     * Изменяет период, за который строим карту.
     *
     * @param {Array} period Массив из двух строк формата Y-m-d
     */
    setPeriod: function(period) {

    /**
     * Изменяет фильтр, которым фильтруем данные.
     *
     * @param {String} filter Строка фильтра, без изменений передаётся на сервер.
     */
    setFilter: function(filter) {

    /**
     * Переключает виджет в режим взаимодействия с сайтом.
     */
    setSiteMode: function() {

    /**
     * Переключает виджет в режим просмотра карты.
     */
    setStatMode: function() {

    /**
     * Возвращает корневой элемент виджета.
     *
     * @return {Node}
     */
    getEl: function() {

    /**
     * Подписывает на событие.
     * Этот метод можно вызывать в том числе на прототипе. Тогда обработчик события будет срабатывать на всех потомках этого прототипа.
     *
     * @param {String} name Имя события.
     * @param {Function} fn Фукнция, вызываемая при возникновении события.
     */
    addEventListener: function(name, fn) {

    /**
     * Отписка от события. Параметры должны быть в точности теми же, что и при подписке.
     *
     * @param {String} name Имя события.
     * @param {Function} fn Подписанный обработчик.
     */
    removeEventListener: function(name, fn) {

### Общие для всех карт события

* load -- возникает при загрузке страницы в карту. В объекте события содержится параметр `url` с адресом страницы, загруженной в ифрейм.


### Параметры и методы `MetrikaInpage.ClickMap`

    /**
     * Тип карты. Значение одно из: heatmap, monochrome, linksandbutton, opacity, elements.
     * @type String
     */
    type: 'heatmap',

    /**
     * Размер кликов при рисовании карты.
     * @type Number
     */
    dotSize: 5,

    /**
     * Прозрачность карты.
     * @type Number
     */
    opacity: 0.5,

    /**
     * Изменяет тип карты. Возможные значения есть выше.
     *
     * @param {String} type
     */
    setType: function(type) {

    /**
     * Изменяет прозрачность карты.
     *
     * @param {Number} opacity
     */
    setOpacity: function(opacity) {

    /**
     * Изменяет размер кликов при рисовании карты.
     *
     * @param {Number} dotSize
     */
    setDotSize: function(dotSize) {

### События `MetrikaInpage.ClickMap`

* clicksinfo -- возникает при изменении данных или количества видимых на экране кликов. Объект события имеет свойства
    * `total` {Number} Всего кликов ever
    * `clicks` {Number} Всего кликов (которыем можно запросить, максимум 32k).
    * `visibled` {Number} Видимых кликов.

### Параметры и методы `MetrikaInpage.ScrollMap`

    /**
     * Тип карты. Значение одно из: heatmap, opacity.
     * @type String
     */
    type: '',

    /**
     * Прозрачность карты.
     * @type Number
     */
    opacity: '',

    /**
     * Изменяет тип карты. Возможные значения есть выше.
     *
     * @param {String} type
     */
    setType: function(type) {

    /**
     * Изменяет прозрачность карты.
     *
     * @param {Number} opacity
     */
    setOpacity: function(opacity) {

### Параметры и методы `MetrikaInpage.LinkMap`

Нет специфичных, только общие для всех карт.

### Примеры

[В папке examples](../../../examples/js)
