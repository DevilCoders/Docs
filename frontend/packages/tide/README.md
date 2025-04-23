# Tide

Tide — инструмент для автоматизации работы с тестами, кодомодификации, генерации, перемещения файлов.
Tide работает с hermione и testpalm тестами, но при желании можно работать с любыми тестами.

### Помощь 👀
 Вопросы? Проблемы? Смело пишите нам в [Slack чат](https://yndx-search.slack.com/archives/CP8P7J6JV)!

## Установка

```
npm i -D @yandex-int/tide --registry=http://npm.yandex-team.ru
```

## Использование

### Настройка

Необходимо создать конфиг в корне проекта с именем `tide.config.js`:
```js
module.exports = {
    plugins: {
        'tide-default-plugin-name': {
            enabled: false
        },
        'tide-plugin-name': {
            enabled: true
        },
        'tide-testpalm-generator': {
            enabled: false,
            rewrite: false,
            replacers: {
                addValue: (args) => [
                    { do: `установить курсор в текстовое поле "${args[0]}"` },
                    { do: `добавить текст в поле "${args[1]}"` }
                ],
                assertView: (args) => ({ screenshot: `внешний вид [${args[0]}]` }),
                back: (args) => ({ do: 'нажать на кнопку "Назад" браузера' }),
                click: (args) => ({ do: `нажать на "${args[0]}"` })
            }
        }
    }
}
```

### Запуск

```
npx tide [options] [command] [paths...]
```

Для дебага используйте переменную окружения `DEBUG`:

```
DEBUG=tide* npx tide [options] [command] [paths...]
```

### Опции

- `-V, --version` — версия пакета
- `-c, --config <path>` — путь до файла конфигурации
- `--ignore <json-array>` — путь до файла(ов) для игнорирования
- `--grep <regexp>` — поиск по имени теста или по регулярному выражению
- `-p, --plugin <paths...>` — путь до плагина-скрипта
- `-s, --silent` — запуск без лога и вывода ошибок (приоритет выше, чем у `--verbose`, default: false)
- `--verbose` — запуск с подробным логом (default: false)
- `--conflict-mode` — режим разрешения конфликтов. Возможные значения: `new|old|both|ask`. Используется, например, в mover и experimenter. 
- `-h, --help` — вывод помощи

### Пути
Для задания путей можно использовать синтаксис [fast-glob](https://github.com/mrmlnc/fast-glob#basic-syntax)

### Команды

- `stats` - статистика по тестовым сценариям (default)
  - `--type [type]` — название типа тестов для подсчета тестов (`'integration'`|`'e2e'`)
  - `--group [key]` — ключ, по которому будут сгруппирован результат (`'tool'`|`testpalmDataKey`, default: `'tool'`)
  - `--tool [tool]` — название инструмента для подсчета тестов для группировки не по `'tool'` (`'testpalm'`|`'hermione'`|`null`, default: `'testpalm'`)
  - `--sort [column|tool.column]` - путь до столбца, по которой будут отсортированы строки (default: `'testpalm.tests'`)
  - `-n, --max-count [number]` - максимальное число строк выводимых в таблице, остальные объединяются в одну строку (default: `0`)

### Плагины

Tide поддерживает расширение функциональности при помощи плагинов.

Плагины подключаются и конфигурируются через `tide.config.js`:

```js
module.exports = {
    plugins: {
        'tide-plugin-name': {
            enabled: true
        }
    }
};
```
Где `tide-plugin-name` — название пакета или путь.

А также плагины можно подключать как скрипты, с помощью опции `-p, --plugin`, указав путь до файла плагина.

```bash
npx tide --plugin path/to/plugin.js
```

Плагин — это функция, внутри которой навешиваются обработчики событий, в которых происходит взаимодействие с коллекциями.

```js
module.exports = (tide) => {
    tide.on(e.BEFORE_FILES_READ, () => {
        console.log('Hello, world!');
    });
};
```

Плагины бывают двух типов:
- парсеры — парсят файлы и добавляют их в коллекции, а потом сериализцую данные перед записью файлов;
- трансформаторы — транформируют данные тестов после чтения и парсинга;

Документация по существующим плагинам представлена в соответствующих директориях:

- [tide-renamer](src/plugins/tide-renamer/README.md)
- [tide-hunter](src/plugins/tide-hunter/README.md)
- [tide-testpalm-generator](src/plugins/tide-testpalm-generator/README.md)
- [tide-testdata-manager](src/plugins/tide-testdata-manager/README.md)
- [tide-experimenter](src/plugins/tide-experimenter/README.md)

#### События

Работа с Tide, включая чтение файлов, получение результатов парсинга, запись, основана на событиях.

| Событие              | Описание |
| -                    | - |
| `CLI`                | Срабатывет перед парсингом CLI-опций. Подходит для расширения CLI-интерфейса. |
| `INIT`               | Инициализация, срабатывает ровно один раз перед запуском всех других действий. |
| `START`              | Начало работы, срабатывает после инициализации testCollection, fileCollection и fileManager. |
| `BEFORE_FILES_READ`  | Срабатывает перед чтением файлов. Подходит для задания файлов, которые нужно прочитать. |
| `AFTER_FILES_READ`   | Срабатывает после чтения и парсинга файлов. Подходит для использования результатов чтения файлов. |
| `BEFORE_FILES_WRITE` | Срабатывает перед записью файлов. |
| `AFTER_FILES_WRITE`  | Срабатывает после записи файлов. |
| `END`                | Срабатывает перед завершением работы. |

Все события, кроме `INIT`, `START` и `END` передают в обработчики `fileManager`, `fileCollection`, `testCollection`. 

### Programmatic API

Tide можно использовать не только как CLI-утилиту, но и программно.

```typescript
import Tide from '@yande-int/tide';
const tide = new Tide(config);
```

`config` - объект, соответствующий формату:

```typescript
interface TideConfig {
    plugins: Record<string, Record<string, any>>;
    ignore?: string[];
}
```

#### `run(): Promise<void>`

Вызов метода `run` запускает Tide:
```typescript
tide.run();
```

#### Пример

Пример получения значения счетчика в заданном testpalm.yml файле.

```typescript
import Tide from '@yandex-int/tide';

const tide = new Tide({ plugins: {} });
const e = tide.events;

tide.on(e.BEFORE_FILES_READ, () => {
    tide.fileManager.setFilePaths('testpalm', ['path/to/file.testpalm.yml']);
});

tide.on(e.AFTER_FILES_READ, () => {
    const counter = tide.fileCollection.getTestFile('path/to/file.testpalm.yml').data.counter;

    console.log(counter);
});

tide.run();
```
