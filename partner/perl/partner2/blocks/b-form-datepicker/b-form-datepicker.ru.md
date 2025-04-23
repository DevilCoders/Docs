Контрол выбора даты. Ошибки показывает средствами b-form-input, который в нем содержится.

###Параметры bemjson
- {string} name
- {string} [value] Дата в формате YYYY-MM-DD
- {string} [minDate] Минимальная возможная дата в формате YYYY-MM-DD
- {string} [maxDate] Максимальная возможная дата в формате YYYY-MM-DD
- {string} [yearRange] Диапазон показываемых годов в формате "-nn:+nn"|"c-nn:c+nn"|"nnnn:nnnn"|"nnnn:-nn", где 'c' - текущий год, 'n'- цифра (http://api.jqueryui.com/datepicker/#option-yearRange). Если диапазон задан, то года не входящие в этот диапазон не будут показыватьcя в выпадающем списке, но при прощелкивании месяцев стрелками будут отображаться даты предыдущих годов, поэтому имеет смысл устанавливать одновременно с minDate & maxDate.
- {string} label
- {string} error

####Моды
- _inline-label_yes Ставит элемент label на одну строку с b-form-input, фиксирует ширину b-form-input
- _width_fixed Фиксирует ширину b-form-input
