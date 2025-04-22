#Грид, позволяющий настраивать корректировки цены клика в зависимости от времени суток

##События

/**
 * Генерируется при начале настройки часов'.
 *
 * @event b-time-targeting-scale-board#brush-down
 */

/**
 * Генерируется при окончании настройки часов'.
 *
 * @event b-time-targeting-scale-board#brush-up
 */

/**
 * Генерируется при выборе ячейки настройки часов. Данное событие запрашивает новый уровень клика для ячейки'.
 *
 * @event b-time-targeting-scale-board#set
 * @param {Object} data данные выбранной ячейки
 * @param {String|Number} data.day день ячейки
 * @param {String} data.hourCode код часа ячейки
 * @param {$.Promise} data.promise промис для получения нового уровня для данной ячейки
 * @param {Boolean} data.isGroupSet было ли выбрано более одной ячейки.
 */

/**
 * Генерируется при выборе чекбокса часа или дня'.
 *
 * @event b-time-targeting-scale-board#checked-line
 * @param {Object} data данные выбора
 * @param {'day'|'hour'} data.type тип чекбокса
 * @param {String|Number} data.value значение выбора
 */

/**
 * Генерируется при снятии чекбокса часа или дня'.
 *
 * @event b-time-targeting-scale-board#unchecked-line
 * @param {Object} data данные выбора
 * @param {'day'|'hour'} data.type тип чекбокса
 * @param {String|Number} data.value значение выбора
 */
