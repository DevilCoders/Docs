# @yandex-id/toolchain

Toolchain for id-frontend

[![oclif](https://img.shields.io/badge/cli-oclif-brightgreen.svg)](https://oclif.io)
[![Version](https://img.shields.io/npm/v/@yandex-id/toolchain.svg)](https://npmjs.org/package/@yandex-id/toolchain)
[![Downloads/week](https://img.shields.io/npm/dw/@yandex-id/toolchain.svg)](https://npmjs.org/package/@yandex-id/toolchain)
[![License](https://img.shields.io/npm/l/@yandex-id/toolchain.svg)](https://github.com/passport-frontend/id-frontend/blob/master/package.json)

<!-- toc -->
* [@yandex-id/toolchain](#yandex-idtoolchain)
* [Commands](#commands)
<!-- tocstop -->

# Commands

<!-- commands -->
* [`monorepo affected COMMAND`](#monorepo-affected-command)
* [`monorepo help [COMMAND]`](#monorepo-help-command)
* [`monorepo publish`](#monorepo-publish)

## `monorepo affected COMMAND`

Команда для запуска npm скриптов на затронутых пакетах

```
USAGE
  $ monorepo affected COMMAND

ARGUMENTS
  COMMAND  Название команды, которую необходимо запустить

OPTIONS
  -h, --help       show CLI help
  --all            Запустить на все узлы
  --linkDependant  Линковать зависимости при запуске
  --master         Запуск на мастере (чтобы захватить изменения последнего ПР)

EXAMPLE
  $ monorepo affected ci:lint --master
```

_See code: [src/commands/affected.ts](https://github.com/passport-frontend/id-frontend/blob/v0.2.0/src/commands/affected.ts)_

## `monorepo help [COMMAND]`

display help for monorepo

```
USAGE
  $ monorepo help [COMMAND]

ARGUMENTS
  COMMAND  command to show help for

OPTIONS
  --all  see all commands in CLI
```

_See code: [@oclif/plugin-help](https://github.com/oclif/plugin-help/blob/v3.3.1/src/commands/help.ts)_

## `monorepo publish`

Команда для публикации измененных пакетов

```
USAGE
  $ monorepo publish

OPTIONS
  -d, --dryRun  Запустить в режиме dryRun, рассказать, что будет делать, но не делать
  -h, --help    show CLI help
  --master      Запуск на мастере (чтобы захватить изменения последнего ПР)
```

_See code: [src/commands/publish.ts](https://github.com/passport-frontend/id-frontend/blob/v0.2.0/src/commands/publish.ts)_
<!-- commandsstop -->
