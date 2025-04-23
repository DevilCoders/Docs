# tide-renamer

Плагин к tide для автоматического переименования тестов. 

Команда `rename`, которую добавляет этот плагин, сканирует проект или указанную директорию, находит тесты,
которые совпадают с заданным названием и производит такие действия:
- переименовывает тесты в файлах hermione;
- переименовывает тесты в файлах testpalm;
- обновляет файлы `.metrics.json`;
- перемещает ассеты внутри `test-data` и `screens` в соответствующие новому названию директории. 

## Установка
Плагин доступен через npm.
```
npm install --save-dev @yandex-int/tide-renamer --registry=http://npm.yandex-team.ru
```

Чтобы включить плагин, необходимо указать его в конфиге tide.

## Использование
Плагин добавляет одну консольную команду:
```
tide rename [path] --old-name <old-name> --new-name <to>
```
`--old-name <old-name>` задает имена тестов, которые нужно переименовать. Поддерживается два формата:
- строка, содержащая полное название теста;
- JSON-массив, содержащий части названия. Элементами JSON-массива могут быть строки,
либо объекты с полями `feature`, `type` и `experiment`.

При передаче массива его элементы считаются регулярными выражениями.

`--new-name <to>` задает новые имена тестов. Как и в случае с `--old-name`, можно передать строку или JSON-массив. Используйте `$n`, чтобы обратиться к подгруппам регулярного выражения.

`[path]` задает путь, внутри которого нужно искать тесты. По умолчанию - весь проект.

### Примеры использования
```
tide -c tide.config.js rename --old-name "Зеленая ссылка / Размер шрифта Внешний вид В обычном режиме" --new-name "Зеленая ссылка / Размер шрифта Внешний вид В абсолютно необычном режиме"
```
В этом случае строка разбивается на части по пробелу и большой букве, при этом перед пробелом не должно быть `'/'`.
Когда нужно разобрать одну из таких частей на поля feature, type, ..., то происходит разбиение по `' / '`.
Если вариантов разбить строку несколько, выбирается наиболее схожий с оригинальным названием. 
```
tide -c tide.config.js rename features/desktop --old-name '[{ "feature": "(Зеленая ссылка)", "experiment": "(Размер шрифта)"}, "(Внешний вид)", "(В обычном режиме)"]' --new-name '[{ "feature": "$1", "experiment": "$1"}, "$1", "$1 и необычном режиме"]'
```

## Конфигурация
Пример `tide.config.js`:
```js
module.exports = {
    plugins: {
        'tide-renamer': {
            testDataDir: (hermioneFilePath) => {
                return path.join(path.dirname(hermioneFilePath), 'test-data');            
            },
            screensDir: (hermioneFilePath) => {
                return path.join(path.dirname(hermioneFilePath), 'screens');
            },
        },
        // ...
    },
};
```
Конфигурация по ключу с путем к tide-renamer может быть пустой, но для включения плагина нужно, чтобы сам ключ присутствовал.
### `(optional) testDataDir(path: string): string`
Функция, принимающая путь к hermione файлу и возвращающая путь к директории test-data.

По умолчанию: при передаче пути `/dir/example.hermione.js` возвращает `/dir/test-data` 

### `(optional) screensDir(path: string): string`
Функция, принимающая путь к hermione файлу и возвращающая путь к директории screens.

По умолчанию: при передаче пути `/dir/example.hermione.js` возвращает `/dir/screens`

## Programmatic API
Класс `TideRenamer` предоставляет программный интерфейс для осуществления переименований тестов.
Ниже приводится список доступных методов и объектов.

### `constructor(tide: Tide, pluginOptions: Partial<TideRenamerOptions>): TideRenamer`
Создает инстанс класса. Принимает на вход инстанс `Tide` и объект конфигурации.
В данный момент `TideRenamerOptions` не имеет доступных полей для использования.

### `getAffectedTests(fromTitlePath: RegExp, toTitlePath: string, tests: Test[]): Test[]`
### `getAffectedTests(fromTitlePath: (RegExp | RegExpObject)[], toTitlePath: (string | StringObject)[], tests: Test[]): Test[]`
Возвращает массив тестов из `tests`, которые изменятся при применении операции переименования `fromTitlePath` => `toTitlePath`.
Примеры вызовов:
```typescript
renamer.getAffectedTests(/^Feature/, 'NewFeature', tests);
renamer.getAffectedTests([
    { feature: /^Feature/, type: /Type (\d+)/}, 'Describe'],
    [{ feature: 'NewFeature', type: 'NewType $1' }, 'New describe'],
    tests
);
```

### `async rename(fromTitlePath: RegExp, toTitlePath: string, tests: Test[]): Promise<void>`
### `async rename(fromTitlePath: (RegExp | RegExpObject)[], toTitlePath: (string | StringObject)[], tests: Test[]): Promise<void>`
Производит переименование тестов из `tests`, выполняя операцию `fromTitlePath` => `toTitlePath`.
Этот метод обновляет все файлы, привязанные к тестам: `hermione`, `testpalm`, `metrics` и файлы ассетов.
Примеры использования:
```typescript
await renamer.rename(/^Feature/, 'NewFeature', tests);
await renamer.rename([
    { feature: /^Feature/, type: /Type (\d+)/}, 'Describe'],
    [{ feature: 'NewFeature', type: 'NewType $1' }, 'New describe'],
    tests
);
```
