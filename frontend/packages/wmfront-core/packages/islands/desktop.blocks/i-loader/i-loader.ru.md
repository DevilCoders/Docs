# i-loader

**Статус блока**: **deprecated**

Блок-помощник для загрузки BEM-бандлов по требованию.

Параметры:

```
* @param {String} [bundleId] Идентификатор бандла. Если не передан будет равен bundlePath
* @param {String} bundlePath Адрес для загрузки бандла
* @param {Function} onSuccess callback-функция на успешную загрузку
* @param {Function} [onError] callback-функция на неуспешную загрузку
* @param {Boolean|String} [lang] Либо флаг о том, что нужно загружать локализованный бандл,
           либо строка ('ru', 'en' и т.д.), указывающая какую конкретно локализацию загружать.
```

### Элементы блока

Элемент | Описание
--- | ---
`bem` | Реализован на уровне `desktop`.


Пример использования:

```javascript
BEM.blocks['i-loader'].load(
    'b-smart-help', // идентификатор бандла
    Lego.params['lego-static-host'] + '/blocks-desktop/b-smart-help/b-smart-help.bembundle.js', // URL бандла
    function() {
        // бандл загрузился
    },
    function() {
        // ошибка
    });
```


