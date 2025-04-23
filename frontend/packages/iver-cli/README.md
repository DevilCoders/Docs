@yandex-int/iver-cli
================

Обертка над @yandex-lego/iver.
Подробнее о работе версионирования читайте в документации iver.

* [Usage](#usage)
* [API](#api)
* [Commands](#commands)

# Usage
<!-- usage -->
```sh-session
$ npm install -g @yandex-lego/iver-cli
$ iver COMMAND
running command...
$ iver (-v|--version|version)
@yandex-lego/iver-cli/0.0.1 darwin-x64 node-v12.18.1
$ iver --help [COMMAND]
USAGE
  $ iver COMMAND
...
```
<!-- usagestop -->

# Commands
<!-- commands -->
- [@yandex-int/iver-cli](#yandex-intiver-cli)
- [Usage](#usage)
- [Commands](#commands)
  - [`iver affected`](#iver-affected)
  - [`iver help [COMMAND]`](#iver-help-command)

## `iver affected`

Команда для вычисления измененных пакетов внутри lerna репозитория

```
USAGE
  $ iver affected

OPTIONS
  -h, --help              show CLI help
  --ignore=ignore         [default: ] Изменения в каких файлах игнорировать
  --lernaIgnore           Дополнить игнор данными из lerna.json command.publish.ignoreChanges
  --noPrivate             Отдавать детальную информацию только для пакетов публикуемых в npm
  --output=(file|stdout)  [default: stdout] куда писать о результатах работы

  --since=since           sha коммита, от которого начать вычислять изменения. Если не передан ищем автокоммит
                          публикации или последний merge.

  --till=till             [default: HEAD] sha коммита, до которого вычислять изменения.

EXAMPLE
  $ iver affected
           {
               "affected": {
                 "@yandex-int/package": {
                   "mergeCommits": [],
                   "directCommits": [],
                   "tag": "npm"
                 }
               }
           }
```

## `iver help [COMMAND]`

display help for iver

```
USAGE
  $ iver help [COMMAND]

ARGUMENTS
  COMMAND  command to show help for

OPTIONS
  --all  see all commands in CLI
```

_See code: [@oclif/plugin-help](https://github.com/oclif/plugin-help/blob/v2.2.3/src/commands/help.ts)_
<!-- commandsstop -->
