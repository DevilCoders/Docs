@yandex-lego/devkit
===================

Инструменты для рефакторинга и написания компонентов. Definitely not bem-tools!

[![oclif](https://img.shields.io/badge/cli-oclif-brightgreen.svg)](https://oclif.io)
[![Version](https://img.shields.io/npm/v/@yandex-lego/devkit.svg)](https://npmjs.org/package/@yandex-lego/devkit)
[![Downloads/week](https://img.shields.io/npm/dw/@yandex-lego/devkit.svg)](https://npmjs.org/package/@yandex-lego/devkit)
[![License](https://img.shields.io/npm/l/@yandex-lego/devkit.svg)](https://github.com/https://github.yandex-team.ru/search-interfaces/frontend/frontend/blob/master/package.json)

<!-- toc -->
* [Usage](#usage)
* [Commands](#commands)
<!-- tocstop -->
# Usage
<!-- usage -->
```sh-session
$ npm install -g @yandex-lego/devkit
$ dk COMMAND
running command...
$ dk (-v|--version|version)
@yandex-lego/devkit/0.1.271 linux-x64 node-v12.18.1
$ dk --help [COMMAND]
USAGE
  $ dk COMMAND
...
```
<!-- usagestop -->
# Commands
<!-- commands -->
* [`dk help [COMMAND]`](#dk-help-command)
* [`dk replacer FILES`](#dk-replacer-files)
* [`dk stat FILES`](#dk-stat-files)

## `dk help [COMMAND]`

display help for dk

```
USAGE
  $ dk help [COMMAND]

ARGUMENTS
  COMMAND  command to show help for

OPTIONS
  --all  see all commands in CLI
```

_See code: [@oclif/plugin-help](https://github.com/oclif/plugin-help/blob/v3.1.0/src/commands/help.ts)_

## `dk replacer FILES`

комманда для замены импортов, названий компонент, а также их пропсов

```
USAGE
  $ dk replacer FILES

ARGUMENTS
  FILES  обрабатываемые файлы

OPTIONS
  -h, --help                   show CLI help
  --handler=handler            обработчик для компонент или пропсов
  --import=import              (required) импорт на который необходимо матчиться
  --newImport=newImport        новый путь до импорта
  --newSpecifier=newSpecifier  новое название для импортируемого компонента
  --parser=parser              [default: tsx] jscodeshift parser
  --specifier=specifier        импортируемый компонент

EXAMPLE
  $ dk replacer
```

## `dk stat FILES`

сбор статистики по импортам и компонентам

```
USAGE
  $ dk stat FILES

ARGUMENTS
  FILES  обрабатываемые файлы

OPTIONS
  -h, --help                 show CLI help
  --concurrency=concurrency  [default: 8] количество одновременно обрабатываемых файлов
  --format=(yml|json)        [default: yml] формат данных

  --package=package          (required) путь или названия компонента для cбора данных (строка или RegExp). Например:
                             lego-on-react, ./components/SomeComponent, @yandex-lego/components/.*

  --props                    дополнительно парсит используемые свойства из JSX

  --reduce                   агрегирует данные по компонентам из всех найденных файлов

  --specifier=specifier      название импортируемого компонента (строка или RegExp). Например: Button, Select

EXAMPLES
  $ dk stat $(find ./src -name *.tsx) --package=lego-on-react
  $ dk stat $(find ./src -name *.tsx) --package=lego-on-react --specifier=Button --props
  $ dk stat $(find ./src -name *.tsx) --package=./src/components/Button/Button --specifier=Button --props --reduce
```
<!-- commandsstop -->
