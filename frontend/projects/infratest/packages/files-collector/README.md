# files-collector

Библиотека для чтения и обработки списка файлов.

## Установка

```bash
npm install @yandex-int/files-collector --save --registry https://npm.yandex-team.ru
```

## Использование
```js
const FilesCollector = require('@yandex-int/files-collector');

(async () => {
    const filesCollector = FilesCollector.create(changedFilesPath);

    // Считает список путей, которые лежат в файле из переменной changedFilesPath и отфильтрует их, используя заданные опции
    const files = await filesCollector.readFiles({include: ['**/*.png'], exclude: ['**/foo/*.png']});

    // Вернет `true`, если среди считанных путей есть путь, в который входит переданная строка и `false` - в противном случае
    const includeFile = filesCollector.includeFile('some-str');
})();

```
### Параметры
* `changedFilesPath` – файл со списком путей, которые хранятся в следующем формате:
```
/some/path/file.png
/some/path/file.js
/some/path/file.txt
```
