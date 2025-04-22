## HtmlTemplateExtras
Добавляет к результату [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin) новый [скрипт](#Пример-скрипта) для подгрузки языковых бандлов текущего языка.

### Настройки

#### langParam
**Обязательный параметр**

Рантайм плейсхолдер текущего языка.

**Тип**: string<br>
**Пример**: `'__webpack_require__.lang'`<br>
**Дефолт**: `'window.lang'`<br>

#### modifyTemplate
**Тип**: boolean | object<br>
**Пример**: `modifyTemplate: { entryFilter: (entry) => entry === 'index' }`<br>
**Дефолт**: `true` (`{ entryFilter: () => true }`) <br>

#### modifyTemplate.entryFilter
Вычисляет, для каких entry нужно генерировать скрипт.
Может быть строкой, равной названию конкретного entry, или функцией от двух аргументов (entryName, templateName).

**Тип**: string | function<br>
**Пример**: `'index'`<br>
**Пример**: `(entry) => entry === 'index'`<br>
**Пример**: 
```js
(entry, template) => {
  switch (template) {
    case 'print': return [ 'vendor', 'print' ].includes(entry);
    case 'index': return [ 'vendor', 'main' ].includes(entry);
    default: return false;
  }
}
```

### Пример скрипта
```html
<script>
if (!window.lang) {
    throw new TypeError('Global lang variable (window.lang) is not set!');
}

(function loadLangAssets(lang) {
    var assets = {
        en: ['i18n.mail-liza.ps-header.en.js'],
        ru: ['i18n.mail-liza.ps-header.ru.js'],
    }[lang];
    var scriptsFragment = assets.reduce(function (fragment, asset) {
        var tag = document.createElement('script');
        tag.type = 'text/javascript';
        tag.src =
            'https://yastatic.net/s3/psf/test-project/' +
            asset;
        fragment.appendChild(tag);
        return fragment;
    }, new DocumentFragment());

    document.querySelector('head').appendChild(scriptsFragment);
})(window.lang);
</script>
```
