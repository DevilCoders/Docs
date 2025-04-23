Позволяет выбрать за что платить и требует ли клид оплаты.

###Параметры для bemjson
- @param {string} **value.selected** Если эквивалентно true, checkbox будет сразу выделен
- @param {string} **value.pay_type_id** Id значения настройки "оплата за"
- @param {string} **value.is_payable_id** Id значения настройки "требует оплаты"
- @param {string} **is_payable.label** Название настройки "требует оплаты"
- @param {object} **is_payable.options** [{id: {string}, label: {string}}] - варианты значений настройки "требует оплаты"
- @param {string} **pay_type.label** Название поля "оплата за"
- @param {object} **pay_type.options** [{id: {string}, label: {string}}] - варианты значений настройки "оплата за"
- @param {string} [**error**] Текст ошибки

###События
- change Возникает при change на checkbox или radio-item (b-form-radio в них).
