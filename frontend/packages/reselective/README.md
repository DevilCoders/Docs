@yandex-int/reselective
=====================

Утилита, позволяющая получить список затронутых блоков в соответствии с измененными файлами.

**Важно:** Если вы в своем проекте по каким-либо причинам импортируете файлы без расширения, утилита будет работать некорректно.

```bash
npm i -DE @yandex-int/reselective
```

* [Конфигурация](#Конфигурация)
* [Adapter](#Adapter)
    - [TSAdapter](#TSAdapter)
* [Matcher](#Matcher)
    - [BemTSMatcher](#BemTSMatcher)

## Конфигурация

### Пример конфигурации

```js
module.exports = {
    adapter: require('@yandex-int/reselective/lib/adapters/ts-adapter')({
        whiteList: ['package.json', '*.conf.js'],
        src: 'src/components',
        mask: ['src/components/**/*.{ts,tsx}'],
    }),
    transforms: {
        hermione: (components) => components.join(' | '),
        unit: (components) => components.join(', '),
    },
    selectiveFileTransform: (components) => components.map((component) => `@yandex-lego/components/${component}`),
};
```

### Опции

#### `--config`

Путь до файла с конфигурацией.

```bash
    reselective run -с ./.config/selective.config.js
```

#### `--execute`

Команда, которую необходимо выполнить, передав в нее результат в качестве опции.
Передавая таким образом команду, пожалуйста, обратите внимание на то, что она должна быть готова принять результат через `--`, например: `npm run unit -- Button Select Popup`.

```bash
    reselective run -e 'npm run unit'
```

#### `--selective-transform`

Определяет необходимост применить к результату коллбек из секции `selectiveTransform` конфигурации.

```bash
    reselective run -s
```

#### `--transform`

Опция указывает, какую из функции-трансформеров необходимо применить к результату.

```bash
    reselective run -t hermione
```

#### `--files`

Список измененных файлов, на основании которых строится список измененных компонентов.

```bash
    reselective run -f Button.css Select.tsx
```

#### `--extended`

Позволяет получить расширенный результат работы `reselective`.

```bash
    reselective run -e
```

Пример вывода:

```js
{
    "directlyAffected": [{
        "entity": {
            "block": "Popup",
            "mod": {
            "name": "theme",
            "val": "normal"
            }
        },
        "tech": "css",
        "layer": "common"
    }],
  "affectedDependents": [
    {
      "entity": { "block": "Showcase" },
      "tech": "examples",
      "layer": "common"
    },
    {
      "entity": { "block": "Showcase" },
      "tech": "tsx",
      "layer": "desktop"
    },
    {
      "entity": { "block": "Showcase" },
      "layer": "touch"
    },
    {
      "entity": { "block": "Showcase" },
      "tech": "tsx",
      "layer": "common"
    },
    {
      "entity": { "block": "Showcase" },
      "tech": "registry",
      "layer": "common"
    },
    {
      "entity": { "block": "Select" },
      "tech": "examples",
      "layer": "common"
    },
    {
      "entity": { "block": "Select" },
      "tech": "bundle",
      "layer": "common"
    },
    {
      "entity": { "block": "Popup" },
      "tech": "examples",
      "layer": "common"
    },
    {
      "entity": { "block": "Popup" },
      "tech": "bundle",
      "layer": "common"
    },
    {
      "entity": { "block": "Popup" },
      "tech": "tests",
      "layer": "common"
    },
    {
      "entity": { "block": "Select" },
      "tech": "tests",
      "layer": "common"
    },
    {
      "entity": { "block": "Popup", "mod": { "name": "theme", "val": "normal" } },
      "tech": "tsx",
      "layer": "common"
    }
  ],
  "plainBlocksList": [
    "Showcase",
    "Select",
    "Popup"
  ]
}
```

### Пример использования в `npm`-скриптах

Можно написать `bash`-обертку, например:

```json
"scripts": {
    "ci:hermione": "AFFECTED=\"$(reselective run -t hermione)\" && [ ! -z \"$AFFECTED\" ] && (npm run hermione:build && LOCAL_PORT=8102 npm run hermione:test -- $AFFECTED) || exit 0",
    "ci:unit": "AFFECTED=\"$(reselective run -t unit)\" && [ ! -z \"$AFFECTED\" ] && npm run unit -- $AFFECTED || exit 0»
}
```

Или можно воспользоватьcя опцией `-e`:

```json
"scripts" {
    "ci:hermione": "reselective run -t hermione -e 'npm run hermione:build && LOCAL_PORT=8102 npm run hermione:test'",
    "ci:unit": "reselective run -t unit -e 'npm run unit'"
}
```

### Adapter

`Adapter` - сущность, которая позволяет получить список затронутых блоков для определенной технологии.

Например, `TSAdapter` строит граф зависимостей на основании импортов в компонентах, а адаптер для `i-bem` мог бы вместо этого использовать `deps.js`.

У `Adapter` обязательно должен быть реализован метод `run()`, который возвращает список затронутых компонентов - именно он вызывается при запуске утилиты.

#### TSAdapter

Адаптер для `TS`-компонентов.
На вход принимает следующие опции:

##### `whiteList`

Массив файлов, при изменении которых нужно запускать все тесты без селективности.

##### `src`

Путь до директории, в которой лежат компоненты.

##### `mask`

`wildcard` для поиска файлов - набора технологий для реализации блоков.
Допустимо передавать: `ts`, `tsx`, `css`, `sass`, `stylus`, `less`, `js`. При этом из файлов `css`, `sass`, `stylus`, `less` импорты забираться не будут.

### packagePath

Путь до пакета, для которого запускается скрипт. По умолчанию - `process.cwd()`.

### matcher

Функция, которая принимает в качестве аргумента опции адаптера и возвращает [матчер]().

### transforms

Функции, которые переводят полученный список блоков в нужный формат для селективного запуска тестов.

### selectiveFileTransform

Функция, преобразующая полученный список блоков в формат экспортов, чтобы этот список можно было передать в пакеты, которые зависят от измененный.


### Matcher

`Matcher` позволяет получить имя компонента из указанного пути до файла.
У `Matcher` обязательно должен быть метод `match`, который в качестве аргумента принимает путь до файла, возвращая имя компонента или `null`.

#### BemTSMatcher

Матчер для работы с файловой структурой, организованной по [методологии БЭМ](https://ru.bem.info/methodology/filestructure/).
