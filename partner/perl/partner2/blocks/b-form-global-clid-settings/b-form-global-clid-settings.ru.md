Позволяет глобально менять параметры всех клидов. Массив зависимых блоков выбора параметров клида (block b-form-clid-settings) передаются в свойство content данного блока во входном bemjson.

###Параметры для bemjson
- @param {string} **is_payable.label** Название настройки "требует оплаты"
- @param {object} **is_payable.options** [{id: {string}, label: {string}}] - варианты значений настройки "требует оплаты"
- @param {string} **pay_type.label** Название поля "оплата за"
- @param {object} **pay_type.options** [{id: {string}, label: {string}}] - варианты значений настройки "оплата за"
