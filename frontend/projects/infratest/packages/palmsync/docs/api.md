# Программное использование

```bash
npm install @yandex-int/palmsync  --registry https://npm.yandex-team.ru
```

## validate

Запускает валидацию тестовых сценариев.

```js
const PalmSync = require('@yandex-int/palmsync');

return PalmSync
    .create()
    .loadPlugins('validate')
    .validate();
```

### loadPlugins

Загружает плагины, которые указаны в секции `plugins.validate` в конфиге `palmsync`.
Подробнее про плагины можно узнать [здесь](#плагины).

## synchronize

Запускает синхронизацию тестовых сценариев.

```js
const PalmSync = require('@yandex-int/palmsync');

return PalmSync
    .create()
    .loadPlugins('synchronize')
    .synchronize();
```

### loadPlugins

Загружает плагины, которые указаны в секции `plugins.synchronize` в конфиге `palmsync`.
Подробнее про плагины можно узнать [здесь](#плагины).

```js
const PalmSync = require('@yandex-int/palmsync');

const palmsync = PalmSync
    .create()
    .loadPlugins();
```

### init

Асинхронный статический метод класса `PalmSync` для инициализации модуля и чтения файлов тестовых сценариев:

* создаёт экземпляр класса;
* загружает тестовые сценарии с файловой системы;
* на основе считанных файлов строит дерево сценариев;
* индексирует тесты для быстрого поиска по полному заголовку и идентификатору браузера.

```js
const PalmSync = require('@yandex-int/palmsync');

PalmSync.init().then((palmsync) => {
    palmsync.findTest('Полный заголовок теста', 'firefox', 'specs');
    palmsync.getTests();
});
```

### readScenarios

Асинхронный метод экземпляра класса `PalmSync` для чтения файлов тестовых сценариев.

```js
const PalmSync = require('@yandex-int/palmsync');

const palmsync = new PalmSync();

palmsync.readScenarios().then((palmsync) => {
    palmsync.findTest('Полный заголовок теста', 'firefox');
    palmsync.getTests();
});
```

### findTest

Метод для поиска теста по его полному заголовку, идентификатору браузера и [типу сценария](./yaml-files.md#Типы-сценариев).

**Примечание** Полное имя состоит из feature тестового сценария,
заголовков всех родительских сьютов и заголовка самого теста разделённых пробелами.

### getTests

Возвращает плоский список всех сценариев.
В качестве необязательного аргумента принимает [тип сценария](./yaml-files.md#Типы-сценариев), благодаря которому вернет сценария только одного типа.
