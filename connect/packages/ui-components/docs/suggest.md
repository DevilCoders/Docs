# Suggest
Компонент для автокомплита

## Параметры

#### disabled `Boolean`
Неактивное состояние

#### defaultValue `String` `Number`
Значение по-умолчанию

#### id `String`
Уникальный идентификатор

#### onBlur(event)
Колбэк потери фокуса
- **event** `ReactEvent`

#### onFocus(event)
Колбэк установки фокуса
- **event** `ReactEvent` 

#### onSelect(data, event)
Колбэк выбора значения
- **data** `Object`
- **event** `ReactEvent`

#### onKeyDown(event)
Колбэк нажатия кнопки

#### placeholder `String`
Текст-подсказка

#### renderItem(data, term) `ReactElement`
Функция рендера элемента списка
- **data** `Object`
- **term** `String`

#### source(term, callback)
Функция запроса данных
- **term** `String`
- **callback** `Function`

#### timeout `Number`
Задержка перед запросом данных (debounce)

#### transparent `Boolean`
Делает поле ввода поле невидимым

#### minLength `Number`
Минимальное кол-во символов для запроса данных

#### name `String`
Название поля ввода

#### size `String`
Размер текстового поля: `s`, `m`, `l`, `xl`

#### value `String` `Number`
Значение поля

#### width `String`
Ширина текстового поля: `available`
