# resource-loader

Обёртка над загружаемыми JS-ресурсами и инлайн-скриптами для контролируемой загрузки/вставки скриптов на страницу.

## Как работает
На сервере вместо вставки скриптов с загружаемыми файлами и инлайн-скриптов с кодом, оборачиваем их в отдельные скрипты resource-loader'а.
Загрузка и вставка таких скриптов происходит в той же очерёдности, что и их вставка на страницу в "обёртке". Пока текущий скрипт не загрузился, следующий скрипт не будет загружаться или исполняться (для инлайн-скриптов) — реализуется очередь загрузки/исполнения скриптов.

## API
1. Инициализация параметров:
```js
resourceLoader.init({
    nonce: '123',
    // Количество попыток загрузки JS-файла
    retry: 2,
    // Таймаут перед повторной попыткой загрузки файла
    retryTimeout: 100,
});

```
2. Добавление скрипта в очередь загрузки/исполнения:
```js
resourceLoader.add({
    // Для загрузки JS-файла
    url: 'https://yastatic.net/react/17.0.2/react-with-dom-and-polyfills.js',
    // Для исполнения инлайн-кода
    content: 'function() { alert(1); }',
    // Атрибуты для тега <script />
    attrs: { crossorigin: '' }
});
```

3. Начать загружать скрипты:
```js
resourceLoader.load();
```

## Как добавить на страницу
1. Вставить основной инлайн-скрипт resource-loader [resource-loader.inline.js](resource-loader.inline.js) (см. `blocks['resource-loader:main']()` в [resource-loader.priv.js](resource-loader.priv.js))
2. Вставить скрипт инициализации [resource-loader-init.inline.js](resource-loader-init.inline.js) (см. `blocks['resource-loader:init'](params)` в [resource-loader.priv.js](resource-loader.priv.js))
3. Добавить на страницу скрипты с помощью обёртки [resource-loader-add.inline.js](resource-loader-add.inline.js) (см. `blocks['resource-loader:wrap-resource'](resource)` в [resource-loader.priv.js](resource-loader.priv.js))
4. Добавить на страницу скрипт начала загрузки [resource-loader-load.inline.js](resource-loader-load.inline.js)  (см. `blocks['resource-loader:load']()` в [resource-loader.priv.js](resource-loader.priv.js)) или, для начала загрузки после инита песочницы Видео [resource-loader-load-on-init.inline.js](resource-loader-load-on-init.inline.js)  (см. `blocks['resource-loader:load-on-init'](params)` в [resource-loader.priv.js](resource-loader.priv.js))
