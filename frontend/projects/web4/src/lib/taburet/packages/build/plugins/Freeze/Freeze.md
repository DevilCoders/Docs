## Freeze

Реализация "фризинга" — переноса собранных файлов в специальную папку.

### FreezeApi

Класс, реализующий метод `freeze`, который умеет переносить файлы из одной папки в другую с сохранением относительного пути или без сохранения.

Сохранение относительного пути может потребоваться, например, для асинхронных модулей, которые подключаются через [динамическим import-ы](https://webpack.js.org/guides/code-splitting/#dynamic-imports). Webpack-рантайм сам обрабатывает эти импорты, используя относительные пути, которые получились при сборке. Если пути изменятся после генерации рантайм-кода, то динамические импорты просто перестанут работать.

```js
// Будем переносить собранные файлы из .build/static в freeze
const api = new FreezeApi({ buildDir: '.build/static', freezeDir: 'freeze' });

// перенос без сохранения относительного пути:
//   .build/static/features/Foo@desktop.hash.js → freeze/Foo@desktop.hash.js
await api.freeze(['features/Foo@desktop.hash.js']);

// перенос с сохранением относительного пути:
//   .build/static/features/Foo@desktop.hash.js → freeze/features/Foo@desktop.hash.js
await api.freeze(['features/Foo@desktop.hash.js'], { keepRelativePath: true });
```

### FreezeChunksPlugin

Плагин фризит файлы для чанков, определенных фильтром:

```js
new FreezeAssetsPlugin({
    // Будем переносить собранные файлы в freeze
    path: 'freeze',

    // Будем переносить файлы чанков, выделенных с помощью SplitChunksPlugin-а
    filter: chunk => chunk.chunkReason,

    // С сохранением относительных путей
    keepRelativePath: true
})
```
