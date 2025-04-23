[О картах активностей](js-libs/Mtrk/Maps/readme.md)

## Вебвизор

### Создание виджета

    var app = new MetrikaInpage.VisorPlayer({
        renderTo: elem,
        counterId: 0,
        date: '20150101',
        visitId: 0,
        hits: [],
        size: [100, 100]
    });
    app.setHit(0); // Запускаем воспроизведение первого хита в визите

Где
* `renderTo` -- dom-элемент, куда поместить виджет
* `visitId` -- идентификатор визита.
* `date` -- дата визита.
* `hits` -- список хитов в визите с краткой информацией о них. Содержится в поле `data` по урлу в апи [/webvisor/v1/data/hits_short](http://trunk.jkee.api.doccenter-dev.yandex.ru/metrika/doc/ref/metrika-api-test2-private/inpage/wvplayer/playhitsshort.xml)
* `size` -- размер виджета, массив вида `[width, height]`

### Методы

    /**
     * Возвращает корневой элемент виджета.
     *
     * @return {Node}
     */
    getEl: function() {

    /**
     * Изменяет размер виджета.
     *
     * @param {Array} size Массив вида [width, height]
     */
    setSize: function(size) {

    /**
     * Переключает плеер к хиту с номером hitNumber.
     * @param {Number} hitNumber
     * @param {Boolean} [isOriginUrl] если true, то хит будет воспроизводиться на текущей версии страницы, иначе в зависимости от настроек вебвизора.
     */
    setHit: function(hitNumber, isOriginUrl) {

    /**
     * Приостанавливает воспроизведение.
     */
    pause: function() {

    /**
     * Запускает воспроизведение после вызова {@link pause}. Должен быть вызван столько раз, сколько был вызван {@link pause}.
     */
    resume: function() {

    /**
     * Устанавливает скорость воспроизведения
     *
     * @param {Number} speedup Коэффициент ускорения. Если меньше 1, то медленнее, больше -- быстрее.
     */
    setSpeedup: function(speedup) {

    /**
     * Перематывает к миллисекунде time.
     *
     * @param {Number} time
     */
    rewind: function(time) {

### События

* hit -- возникает при начале нового хита. Свойства: `hitNumber`.
* tick -- возникает при изменении текущего момента в хите (для полоски прогресса). Свойства: `now` -- количество милисекунд от начала хита.
* pageconnect -- установили связь со страницей
* pagedisconnect -- потеряли связь со страницей
* archivestatus -- возникает, когда становится известно о статусе страницы в плеере. Свойства: `status` -- `false`, если текущая версия страницы, `true`, если страница, сохранённая в момент записи хита, объект `Date`, если страница, скачанная метриковским архиватором в этот момент времени.
