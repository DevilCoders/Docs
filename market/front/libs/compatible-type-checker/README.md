# compatible-type-checker

Компонент проверки обратной совместимости API файлов двух версий. Проверяются совместимость Flow-типов, которые в них задекларированы.
Flow-типы преобразуются в JSON-схему с помощью [flow2schema](https://github.yandex-team.ru/market/flow2schema), затем проверяются на совместимость с помощью [json-schema-diff-validator
](https://github.yandex-team.ru/market/json-schema-diff-validator).

## Установка
```shell script
npm i @yandex-market/compatible-type-checker
```

## Програмный интерфейс:
Проверка совместимости между текущей и базовой (`master`) ветками Git:
```js
// @flow
import {check, type Options, type CheckResult} from 'compatible-type-checker';


const options: Options = {
    files: '*.js',
    ignore: '*.flow.js',
    checkVersion: 'check',
};

const result: CheckResult = check(options);

console.log(result.compatible); // True | False
```

Проверка совместимости между двумя директориями:
```js
// @flow
import {check, type Options, type CheckResult} from 'compatible-type-checker';


const options: Options = {
    files: '*.js',
    ignore: '*.flow.js',
    actualVersion: 'actual',
    checkVersion: 'check',
};

const result: CheckResult = check(options);

console.log(result.compatible); // True | False
```

### Опции:
#### `actualVersion: string = undefined`
Путь к файлам актуальной версии API. Если параметр не указан, будет предпринята попытка проверки веток Git.

#### `actualBranch: string = 'master'`
Ветка с актуальной версией API.

#### `actualBootstrapCmd: string = undefined`
Команда, которая будет выполнена в директории актуальной ветки перед проверкой совместимости.

#### `cache: boolean = false`
Если параметр указан, актуальная ветка будет закэширована при первом запуске проверки совместимости.

#### `checkVersion: string = process.cwd()`
Путь к файлам проверяемой версии API. По умолчанию соответствует текущей рабочей директории.

#### `files: string = '.*js'`
[Шаблон файлов](https://github.com/isaacs/node-glob#glob-primer) для проверки API.

#### `ignore: string = ''`
[Шаблон файлов](https://github.com/isaacs/node-glob#glob-primer), которые будут исключены из проверки.

#### `exports: string[] = ['Params', 'Result']`
Имена типов, которые необходимо проверять. Если параметр имеет тип `void`, будут проверятся все экспортируемые файлами типы (flow2schema).

#### `allowExtendedProperties: boolean = true`
Разрешить расширенные свойства в JSON-схеме (flow2schema).

#### `lib: string[] = void`
Список путей к внешним библиотекам. Позволяет правильно резолвить типы зависимостей (flow2schema).

#### `sourceModuleExtensions: string[] = ['.js']`
Список расширений файлов с исходниками (flow2schema).

#### `extendedPropertiesList: string[] = []`
Список разрешенных расширенных свойств JSON-схемы (flow2schema).

#### `allowNewOneOf: boolean = true`
New oneOf/anyOf items are considered a backwards compatible change (json-schema-diff-validator).

#### `allowNewEnumValue: boolean = true`
New enum values are considered a backwards compatible change (json-schema-diff-validator).

#### `allowReorder: boolean = true`
Reordering of anyOf items are considered a backwards compatible change (json-schema-diff-validator).

## CLI-интерфейс:

```shell script
compatible-type-checker help # справочник по командам и параметрам
compatible-type-checker # проверка совместимости текущей ветки с веткой master для репозитория из текущего каталога
compatible-type-checker --av "actual" --cv "check" -f "*.js" -i "*.flow.js" -p "list" -0 "output.json" # проверка совместимости между файлами двух директорий
```

#### Параметры командной строки:

#### `--version (-v)`
Выводит верссию модуля.
#### `--strict (-s)`
Строгий режим. При включенном режиме если API оказываются несовместимыми, выполнение команды завершается кодом 1. В противном случае кодом 0. По умолчанию используется нестрогий режим.
#### `--output (-o)`
Путь к файлу, куда будет сохранён отчет (тип `CheckResult`). По умолчанию результат выводится в stdout.
#### `--reporter (-r)`
Тип отчета. Поддерживаются значения: `list` - консольный отчет со списком проверенных файлов, `json` - исходные данные результата проверки в формате JSON (значение по умолчанию). 
#### `--config (-c)`
Путь к конфигурационному файлу в формате JSON.
#### `--actualVersion (--av)`
Опция `actualVersion`.
#### `--actualBranch (-b)`
Опция `actualBranch`.
#### `--actualBootstrapCmd (--abc)`
Опция `actualBootstrapCmd`.
#### `--cache (--ch)`
Опция `cache`.
#### `--checkVersion (--cv)`
Опция `checkVersion`.
#### `--files (-f)`
Опция `files`.
#### `--ignore (-i)`
Опция `ignore`.
#### `--exports (-e)`
Опция `exports`.
#### `--allowExtendedProperties (--ep)`
Опция `allowExtendedProperties`.
#### `--lib (-l)`
Опция `lib`.
#### `--sourceModuleExtensions (--me)`
Опция `sourceModuleExtensions`.
#### `--extendedPropertiesList (--pl)`
Опция `extendedPropertiesList`.
#### `--allowNewOneOf (--ao)`
Опция `allowNewOneOf`.
#### `--allowNewEnumValue (--ae)`
Опция `allowNewEnumValue`.
#### `--allowReorder (--ar)`
Опция `allowReorder`.
