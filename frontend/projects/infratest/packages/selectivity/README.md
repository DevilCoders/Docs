# selectivity

> ⚠️ WIP

Общий инструмент обеспечивающий селективный запуск проверок в CI в проектах и сервисах frontend-а.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Установка](#%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0)
- [Использование](#%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)
  - [CLI](#cli)
    - [calc](#calc)
    - [validate](#validate)
  - [API](#api)
    - [.calc](#calc)
    - [.validate](#validate)
    - [Опции](#%D0%BE%D0%BF%D1%86%D0%B8%D0%B8)
  - [Конфигурация](#%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8F)
    - [Ключевые поля](#%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%B2%D1%8B%D0%B5-%D0%BF%D0%BE%D0%BB%D1%8F)
    - [Маркеры](#%D0%BC%D0%B0%D1%80%D0%BA%D0%B5%D1%80%D1%8B)
    - [Несколько конфигурационных файлов](#%D0%BD%D0%B5%D1%81%D0%BA%D0%BE%D0%BB%D1%8C%D0%BA%D0%BE-%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D0%BE%D0%BD%D0%BD%D1%8B%D1%85-%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2)
    - [Динамические маркеры](#%D0%B4%D0%B8%D0%BD%D0%B0%D0%BC%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B5-%D0%BC%D0%B0%D1%80%D0%BA%D0%B5%D1%80%D1%8B)
    - [Маркер `*`](#%D0%BC%D0%B0%D1%80%D0%BA%D0%B5%D1%80-)
  - [Вывод результата](#%D0%B2%D1%8B%D0%B2%D0%BE%D0%B4-%D1%80%D0%B5%D0%B7%D1%83%D0%BB%D1%8C%D1%82%D0%B0%D1%82%D0%B0)
  - [Валидация](#%D0%B2%D0%B0%D0%BB%D0%B8%D0%B4%D0%B0%D1%86%D0%B8%D1%8F)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Установка

```bash
$ npm install @yandex-int/selectivity
```

## Использование

### CLI

Чтобы получить полную информацию по `CLI` инструмента, достаточно выполнить:

```bash
$ selectivity --help
```

#### calc

Выполнить:

```bash
$ selectivity calc --help
```

В выводе будет информация по использованию команды:

```bash
selectivity calc [paths...]

Selectivity based on code changes

Positionals:
  paths  List of files and/or dirs that can be instead passed from standard input  [array] [default: []]

Options:
  --help, -h       Show help  [boolean]
  --version, -v    Show version number  [boolean]
  --config, -c     Path to a config file  [string] [default: ".selectivity.conf.js|.json|.yaml|.yml"]
  --output-format  Output format  [string] [choices: "json"] [default: "json"]

Examples:
  selectivity file1 file2             Pass files as arguments
  echo 'file1 file2' | selectivity    Pass files from standard input in one line
  git diff --name-only | selectivity  Pass files from standard input in several lines
```

#### validate

Выполнить:

```bash
$ selectivity validate --help
```

В выводе будет информация по использованию команды:

```bash
selectivity validate [paths...]

Checks whether file and/or dir paths are described in a config

Positionals:
  paths  List of files and/or dirs that can be instead passed from standard input  [array] [default: []]

Options:
  --help, -h      Show help  [boolean]
  --version, -v   Show version number  [boolean]
  --config, -c    Path to a config file  [string] [default: ".selectivity.conf.js|.json|.yaml|.yml"]
  --reporter, -r  Reporter type  [choices: "flat"] [default: "flat"]

Examples:
  selectivity validate .                       Pass cwd as argument
  selectivity validate file dir                Pass files and/or dirs as arguments
  echo 'file dir' | selectivity validate       Pass files and/or dirs from standard input in one line
  git diff --name-only | selectivity validate  Pass files and/or dirs from standard input in several lines

```

Подробнее о валидации в отдельном [разделе](#валидация).

### API

#### .calc

- **{String[]}**: список файлов
- **{String}**: путь до конфигурационного файла
- **{Object}**: [опции](#Опции)
- `returns` **{Object}**: [результат](#Вывод-результата)

```javascript
const selectivity = require("@yandex-int/selectivity");

const options = { cwd: process.cwd() };

selectivity.calc(["foo/bar", "baz/quux"], ".selectivity.conf.js", options).then((res) => console.log(res));
```

#### .validate

Проверка покрытия паттернами из конфига указанных файлов и/или директорий. 

- **{String[]}**: список файлов и/или директорий
- **{String}**: путь до конфигурационного файла
- **{Object}**: [опции](#Опции)
- `returns` **{Error[]}**: список ошибок

```javascript
const selectivity = require('@yandex-int/selectivity');

const options = { cwd: process.cwd() };

selectivity.validate(["foo/bar", "baz/quux"], ".selectivity.conf.js", options).then((errors) => console.log(errors));
```

Подробнее о валидации в отдельном [разделе](#валидация).

#### Опции

| **Опция** | **Тип** | **Значение по умолчанию** | **Описание** |
| --- | --- | --- | --- |
| `cwd` | `String` | `process.cwd()` | Текущая рабочая директория |

### Конфигурация

Конфигурационный файл представляет собой объект, который состоит из ключевых полей и полей-маркеров.
Названия полей-маркеров никак не привязаны к инструменту, определяются пользователем и будут содержаться в выводе результата выполнения программы, на который могут опираться другие утилиты. Ключевые поля являются зарезервированными в рамках инструмента и используются для конфигурации полей-маркеров и их значений.

#### Ключевые поля

- `root` - путь, относительно которого резолвятся все пути, указанные в конфигурационном файле; по умолчанию: директория, в которой находится конфигурационный файл

#### Маркеры

За основу возьмем псевдомонорепозиторий на базе `lerna`, где проекты лежат в `packages/*` и `services/*`:

```bash
frontend/
├── .selectivity.conf.js
├── lerna.json
├── package.json
├── packages
│   ├── package1
│   └── package2
└── services
    ├── service1
    └── service2
```

Рассмотрим пример конфигурации в файле `.selectivity.conf.js` для `services/service1`:

```javascript
module.exports = {
    root: ".",
    projects: {
        "services/service1":  {
            root: "services/service1",
            scripts: {
                "ci:unit": [
                    "src/**",
                ],
                "ci:hermione": {
                    // root: "services/services1", // если не указывать, то будет унаследован верхнеуровневый "root"
                    platforms: {
                        desktop: [
                            "src/**/*@desktop.tsx",
                        ],
                        touch: [
                            "src/**/*@touch.tsx",
                        ],
                    },
                },
            },
        },
    },
};
```

В конфиге выше указан маркер `projects`, в который вложен маркер `services/service1`. Значением маркера `services/services1` является другой конфиг:

```javascript
{
    root: "services/service1",
    scripts: { ... },
}
```

Во вложенном конфиге переопределено ключевое поле `root` и указан маркер `scripts` (маркер `scripts` считается вложенным в маркер `services/service1`).

Маркер `ci:unit` вложен в `scripts` и матчится на список соответствующих паттернов, маркер `ci:hermione` тоже вложен в `scripts`, а значением маркера является другой конфиг (как видно, конфиги могут быть сколь угодно вложенными):

```javascript
{
    platforms: { ... },
}
```

В этом конфиге указан маркер `platforms` и не указано ключевое поле `root`, поэтому его значение унаследуется из дочернего конфига и определится как `services/service1`.
И наконец, маркеры `desktop` и `touch` вложены в маркер `platforms` и матчатся на список соответствующих паттернов.

Точно таким же образом можно сконфигурировать остальные проекты:

```javascript
module.exports = {
    root: ".",
    projects: {
        "services/service1": { ... },
        "services/service2": { ... },
        "packages/package1": { ... },
        "packages/package2": { ... },
    },
};
```

#### Несколько конфигурационных файлов

Конфигурация каждого проекта монорепозитория в одном файле приведёт к тому, что конфиг будет громозтким, так как проектов может стать очень много, поэтому предоставлена возможность указывать путь до вложенного конфига из основного конфига:

```javascript
module.exports = {
    projects: {
        "services/service1": "services/service1/.selectivity.conf.js",
        "services/service2": "services/service2/.selectivity.conf.js",
        "packages/package1": "packages/package1/.selectivity.conf.js",
        "packages/package2": "packages/package2/.selectivity.conf.js",
    },
};
```

При этом один и тот же конфиг не может использоваться разными маркерами, то есть следующий конфиг:

```javascript
module.exports = {
    projects: {
        "services/service1": "foo/bar/.selectivity.conf.js",
        "services/service2": "foo/bar/.selectivity.conf.js",
    },
};
```

приведет к ошибке, так как конфиг `foo/bar/.selectivity.conf.js` не может быть использован и для маркера `services/service1`, и для маркера `services/service2`.

#### Динамические маркеры

Чтобы каждый раз при добавлении нового проекта в монорепозиторий не нужно было обновлять основной конфиг, существует возможность указывать маркеры и пути ко вложенным конфигам через динамические паттерны:

```javascript
module.exports = {
    projects: {
        "services/*": "services/*/.selectivity.conf.js",
        "packages/*": "packages/*/.selectivity.conf.js",
    },
};
```

что эквивалентно

```javascript
module.exports = {
    projects: {
        "services/service1": "services/service1/.selectivity.conf.js",
        "services/service2": "services/service2/.selectivity.conf.js",
        "packages/package1": "packages/package1/.selectivity.conf.js",
        "packages/package2": "packages/package2/.selectivity.conf.js",
    },
};
```

Динамический маркер представляет из себя пару ключ-значение, где ключ - это [динамический](https://github.com/mrmlnc/fast-glob#what-is-a-static-or-dynamic-pattern) или статический паттерн для директорий, а значение - это динамический паттерн для конфигурационных файлов, которые лежат в соответствующих директориях:

```javascript
module.exports = {
    projects: {
        "services/*": "services/*/.selectivity.conf.js", // динамический маркер

        // приведённый ниже маркер не является динамическим,
        // так как "foo/bar/.selectivity.conf.js" не является динамическим паттерном,
        // поэтому имя маркера "packages/*" интерпретируется как есть
        "packages/*": "foo/bar/.selectivity.conf.js",
    },
};
```

При этом, чтобы обеспечить однозначное соответствие между динамическими ключами и их динамическими значениями, наложены следующие ограничения/правила:
- пути, которые матчатся на значение динамического маркера, должны находится внутри директорий, которые матчатся на ключ динамического маркера:
  ```javascript
  module.exports = {
      projects: {
          // если будут найдены файлы, которые матчатся на "packages/*/.selectivity.conf.js",
          // и директории, которые матчатся на "services/*", то вылетит ошибка,
          // так как найденные файлы не находятся внутри найденных директорий
          "services/*": "packages/*/.selectivity.conf.js",
      },
  };
  ```
- пути, которые матчатся на ключ динамического маркера, должны содержать только один соответствующий конфиг, который матчится на значение динамического маркера:
  ```javascript
  module.exports = {
      projects: {
          // если будет найдено несколько файлов, которые матчатся на
          // "services/service1/.services.conf.(js|json)", то вылетит ошибка,
          // так как инструмент не может определить, какой из конфигов использовать
          "services/service1": "services/service1/.services.conf.(js|json)",
      },
  };
  ```
- пути, которые матчатся на ключи динамических маркеров, не должны пересекаться:
  ```javascript
  module.exports = {
      projects: {
          // если паттерны "services/*" и "services/service1*"
          // сматчатся на пересекающиеся директории,
          // то вылетит ошибка, так как инстурмент не может определить,
          // какой из маркеров имеет больший приоритет
          "services/*": "services/*/.selectivity.conf.js",
          "services/service1*": "services/service1*/.selectivity.conf.json",
      },
  };
  ```
- пути, которые матчатся на значения динамических маркеров, не должны пересекаться:
  ```javascript
  module.exports = {
      projects: {
          // если паттерны "services/service1/packages/package1/.selectivity.conf.*" и
          // "services/service1/packages/package1/.selectivity.conf.(js|yaml)"
          // сматчатся на одни и те же конфигурационные файлы,
          // то вылетит ошибка, так как инструмент не может использовать
          // один и тот же конфигурационный файл для нескольких маркеров
          "services/service1": "services/service1/packages/package1/.selectivity.conf.*",
          "services/service1/packages/package1": "services/service1/packages/package1/.selectivity.conf.(js|yaml)",
      },
  };
  ```
- пути, которые матчатся на значения динамических маркеров, не должны пересекаться с путями статических маркеров:
  ```javascript
  module.exports = {
      projects: {
          // если паттерн "services/service1/packages/package1/.selectivity.conf.*" сматчится
          // на файл "services/service1/packages/package1/.selectivity.conf.js",
          // то вылетит ошибка, так как инструмент не может использовать
          // один и тот же конфигурационный файл для нескольких маркеров
          "services/service1": "services/service1/packages/package1/.selectivity.conf.*",
          "services/service1/packages/package1": "services/service1/packages/package1/.selectivity.conf.js",
      },
  };
  ```
- если пути, которые матчатся на ключ динамического маркера, не содержат конфиг, который матчится на значение динамического маркера, то будет использован конфиг по умолчанию:
  ```javascript
  module.exports = {
      root: ".",
      projects: {
          "services/*": "services/*/.selectivity.conf.js",
      },
  };
  ```
  Если паттерн `services/*` сматчится на `services/service1`, а файла `services/service1/.selectivity.conf.js` не будет существовать, то конфиг раскроется в
  ```javascript
  module.exports = {
      root: ".",
      projects: {
          "services/service1": {
              root: "services/service1", // "root" соответствует сматченной директории
          },
      },
  };
  ```
- `**` интерпретируются как `*` в паттернах:
  ```javascript
  module.exports = {
      projects: {
          "services/**": "services/**/.selectivity.conf.js",
          // динамический маркер выше эквивалентен
          // "services/*": "services/*/.selectivity.conf.js",
      },
  };
  ```
- статические маркеры имеют больший приоритет, чем динамические маркеры:
  ```javascript
  module.exports = {
      projects: {
          // если паттерны "services/*" и "services/*/.selectivity.conf.js"
          // сматчатся на "services/service1" и "services/service1/.selectivity.conf.js",
          // то маркер "services/service1" всё равно будет использовать конфиг
          // "foo/bar/.selectivity.conf.js"
          "services/*": "services/*/.selectivity.conf.js",
          "services/service1": "foo/bar/.selectivity.conf.js",
      },
  };
  ```

#### Маркер `*`

Чтобы избежать дублирования в значениях маркеров, в конфиге существует возможность выносить общие паттерны и общие части конфига в маркер `*`, при этом маркер `*` можно указать на любом уровне вложенности:

```javascript
module.exports = {
    root: ".",
    "*": ["package.json", "!README.md"],
    projects: {
        "*": {
            "*": {
                "ci:unit": ["mocha.opts"],
                "ci:hermione": {
                    platforms: {
                        "*": [".hubby.conf.js"],
                    },
                },
            },
        },
        "services/services1": {
            root: "services/services1",
            scripts: {
                "ci:unit": ["src/**"],
                "ci:hermione": {
                    platforms: {
                        desktop: [
                            "src/**/*@desktop.tsx",
                        ],
                        touch: [
                            "src/**/*@touch.tsx",
                        ],
                    },
                },
            },
        },
    },
};
```

что эквивалентно

```javascript
module.exports = {
    root: ".",
    projects: {
        "services/services1": {
            root: "services/services1",
            scripts: {
                "ci:unit": [
                    "src/**",
                    "../../mocha.opts",
                    "../../package.json",
                    "!../../README.md",
                ],
                "ci:hermione": {
                    platforms: {
                        desktop: [
                            "src/**/*@desktop.tsx",
                            "../../.hubby.conf.js",
                            "../../package.json",
                            "!../../README.md",
                        ],
                        touch: [
                            "src/**/*@touch.tsx",
                            "../../.hubby.conf.js",
                            "../../package.json",
                            "!../../README.md",
                        ],
                    },
                },
            },
        },
    },
};
```

Кроме того, через маркер `*` можно зафиксировать общий формат маркеров, чтобы гарантировать их наличие во всех остальных маркерах, которые маркер `*` дополняет. Рассмотрим пример:

```javascript
module.exports = {
    root: ".",
    projects: {
        "*": {
            "scripts": {
                "ci:unit": [],
                "ci:hermione": {
                    platforms: {
                        desktop: [],
                        touch: [],
                    },
                },
            },
        },
        "services/service1": {
            root: "services/services1",
            scripts: {
                "ci:unit": ["src/**"],
            },
        },
        "services/service2": {
            root: "services/service2"
        },
    },
};
```

Для маркера `services/service1` явно не указан маркер `ci:hermione` (и его вложенные маркеры), а для маркера `services/service2` явно не указан `scripts` (и его вложенные маркеры), но маркер `*` содержит дополнение и для маркера `services/service1`, и для маркера `services/service2`, поэтому конфиг выше будет эквивалентен следующему конфигу:

```javascript
module.exports = {
    root: ".",
    projects: {
        "services/services1": {
            root: "services/services1",
            scripts: {
                "ci:unit": ["src/**"],
                "ci:hermione": {
                    platforms: {
                        desktop: ["**"],
                        touch: ["**"],
                    },
                },
            },
        },
        "services/service2": {
            root: "services/service2",
            scripts: {
                "ci:unit": ["**"],
                "ci:hermione": {
                    platforms: {
                        desktop: ["**"],
                        touch: ["**"],
                    },
                },
            },
        },
    },
};
```

Данный подход позволяет
- в проектах, в которых не собираются настраивать селективность (или пока её не настроили), безусловно матчится на все маркеры и, следовательно, запускать все проверки
- в проектах, в которых не указали какой-то маркер или указали его некорректно, безусловно матчится на этот маркер, и следовательно, запускать соответствующие ему проверки

### Вывод результата

В качестве результата инструмент выводит в `stdout` иерархию маркеров, которые соответствуют переданному на вход списку файлов. Рассмотрим пример:

```javascript
module.exports = {
    projects: {
        "services/services1": {
            root: "services/services1",
            scripts: {
                "*": ["!README.md"],
                "ci:unit": ["tests/**"],
                "ci:hermione": {
                    platforms: {
                        desktop: ["hermione/desktop/**"],
                        touch: ["hermione/touch/**"],
                    },
                },
            },
        },
    },
};
```

Конфиг выше и переданный на вход список файлов:

```bash
services/service1/README.md
services/service1/tests/unit.js
services/service1/hermione/touch/touch.js
```

сгенерируют следующий `output`, например, в json-формате:

```json
{
    "projects": {
        "services/service1": {
            "scripts": {
                "ci:unit": [
                    "services/service1/tests/unit.js"
                ],
                "ci:hermione": {
                    "platforms": {
                        "touch": [
                            "services/service1/hermione/touch/touch.js"
                        ]
                    }
                }
            }
        }
    }
}
```

### Валидация

Суть валидации заключается в том, чтобы проверить, что каждый из переданных на вход файлов и/или каждый из файлов в переданных на вход директориях матчится хотя бы на один позитивный или негативный паттерн из конфига. Рассмотрим пример:

```javascript
module.exports = {
    projects: {
        "services/services1": {
            root: "services/services1",
            scripts: {
                "*": ["!README.md"],
                "ci:unit": ["tests/**"],
                "ci:hermione": {
                    platforms: {
                        desktop: ["hermione/desktop/**"],
                    },
                },
            },
        },
    },
};
```

Конфиг выше и переданный на вход список файлов:

```bash
services/services1/README.md
services/services1/tests/unit.js
services/services1/hermione/touch/touch.js
```

приведут к ошибке валидации, так как файл `services/service1/hermione/touch/touch.js` не покрывается ни одним из паттеров в соответствующем конфиге. Однако, cтоит обратить внимание на то, что файл `services/services1/README.md` считается покрытым паттернами из конфига, так как существует негативный паттерн, который матчится на этот файл.
