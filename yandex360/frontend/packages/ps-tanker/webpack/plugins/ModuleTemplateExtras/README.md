## ModuleTemplateExtras
Добавляет к webback рантайму (webpack/MainTemplate) новую часть, которая отключает подгрузку ненужных языковых чанков.<br>
Выставляет внутреннюю webpack переменную для ссылки на текущий язык. 

### Настройки

#### langParam
**Обязательный параметр**

Рантайм плейсхолдер текущего языка.

**Тип**: string<br>
**Пример**: `'__webpack_require__.l'`<br>
**Дефолт**: `'window.lang'`<br>

### Пример скрипта
```js
// setup webpack internal lang variable
if (!window.lang) {
  throw new TypeError('Global lang variable (window.lang) is not set!');
}
__webpack_require__.l = window.lang;

(function (langs) {
  // mute unused langs
  for (var key in langs) {
    if (key !== __webpack_require__.l) {
      window['webpackJsonp'].push([langs[key], {}]);
    }
  }
})({
  en: ['i18n.mail-liza.ps-header.en', 'i18n.mail-liza.ps-sidebar.en'],
  ru: ['i18n.mail-liza.ps-header.ru', 'i18n.mail-liza.ps-sidebar.ru'],
});
```
