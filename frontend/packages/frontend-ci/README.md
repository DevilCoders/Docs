frontend-ci
=================

> ⚠️ Обязательно обратите внимание на файл [`CONTRIBUTING.md`](./CONTRIBUTING.md), чтобы узнать о том, как разрабатывать и тестировать этот пакет.

Set of CI tools for Frontend monorepo

<!-- toc -->
* [Usage](#usage)
* [Commands](#commands)
<!-- tocstop -->
# Usage
<!-- usage -->
```sh-session
$ npm install -g @yandex-int/frontend-ci
$ frontend-ci COMMAND
running command...
$ frontend-ci (-v|--version|version)
@yandex-int/frontend-ci/2.17.6 linux-x64 node-v12.18.1
$ frontend-ci --help [COMMAND]
USAGE
  $ frontend-ci COMMAND
...
```
<!-- usagestop -->
# Commands
<!-- commands -->
* [`frontend-ci archive-pr-experiments`](#frontend-ci-archive-pr-experiments)
* [`frontend-ci bootstrap`](#frontend-ci-bootstrap)
* [`frontend-ci check-templates`](#frontend-ci-check-templates)
* [`frontend-ci ci:deploy`](#frontend-ci-cideploy)
* [`frontend-ci ci:deploy:master`](#frontend-ci-cideploymaster)
* [`frontend-ci ci:deploy:release`](#frontend-ci-cideployrelease)
* [`frontend-ci ci:deploy:remove`](#frontend-ci-cideployremove)
* [`frontend-ci ci:pulse:build`](#frontend-ci-cipulsebuild)
* [`frontend-ci ci:pulse:shooter`](#frontend-ci-cipulseshooter)
* [`frontend-ci ci:pulse:static`](#frontend-ci-cipulsestatic)
* [`frontend-ci ci:testpalm:suite`](#frontend-ci-citestpalmsuite)
* [`frontend-ci ci:testpalm:synchronize`](#frontend-ci-citestpalmsynchronize)
* [`frontend-ci ci:testpalm:synchronize:testing`](#frontend-ci-citestpalmsynchronizetesting)
* [`frontend-ci ci:testpalm:validate`](#frontend-ci-citestpalmvalidate)
* [`frontend-ci ci:unit`](#frontend-ci-ciunit)
* [`frontend-ci config NAME`](#frontend-ci-config-name)
* [`frontend-ci enable-skipped-tests`](#frontend-ci-enable-skipped-tests)
* [`frontend-ci expflags-sync`](#frontend-ci-expflags-sync)
* [`frontend-ci expflags-to-testids`](#frontend-ci-expflags-to-testids)
* [`frontend-ci format-jobs-data`](#frontend-ci-format-jobs-data)
* [`frontend-ci get-changes-in-workcopy`](#frontend-ci-get-changes-in-workcopy)
* [`frontend-ci get-muted-checks`](#frontend-ci-get-muted-checks)
* [`frontend-ci help [COMMAND]`](#frontend-ci-help-command)
* [`frontend-ci install-root`](#frontend-ci-install-root)
* [`frontend-ci internal:run-on-leaf`](#frontend-ci-internalrun-on-leaf)
* [`frontend-ci leaves:fetch-modules`](#frontend-ci-leavesfetch-modules)
* [`frontend-ci leaves:publish-modules`](#frontend-ci-leavespublish-modules)
* [`frontend-ci pr-experiment`](#frontend-ci-pr-experiment)
* [`frontend-ci publish-mq-artifacts`](#frontend-ci-publish-mq-artifacts)
* [`frontend-ci workspace ACTION`](#frontend-ci-workspace-action)

## `frontend-ci archive-pr-experiments`

Archiving all created experiments for PR.

```
USAGE
  $ frontend-ci archive-pr-experiments

OPTIONS
  --dry-run              Displays the operations that would be performed using the specified command without actually
                         running them.

  --pr-number=pr-number  (required) Pull Request ID
```

## `frontend-ci bootstrap`

Инициализирует листья монорепозитория

```
USAGE
  $ frontend-ci bootstrap

OPTIONS
  --cache-path=cache-path    [default: /place/sandbox-data/tasks/2/7/1381630072/arc_mount/frontend/packages/npm_cache]
                             Путь до папки с npm-кэшом

  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU

  --[no-]force-filtered      Форсирует bootstrap dependencies и dependents

  --ignore-cache             Не использовать npm-кэш из Sandbox ресурса

  --leaf=leaf                Имя листа

  --lfs                      Скачать lfs файлы

  --publishNpmCache          Опубликовать результирующий npm cache как Sandbox ресурс

  --since=since              SHA коммита, от которого вычисляются измененные листья

EXAMPLES
  $ frontend-ci bootstrap --since 389782f83850224f06016fb85e4f301985b002fe
  $ frontend-ci bootstrap --leaf @yandex-ind/test-pkg
  $ frontend-ci bootstrap --leaf @yandex-ind/test-pkg --lfs
  $ frontend-ci bootstrap --leaf @yandex-ind/test-pkg --lfs --publishNpmCache
```

## `frontend-ci check-templates`

Запускает произвольный скрипт на каждом листе из фильтра

```
USAGE
  $ frontend-ci check-templates

OPTIONS
  --concurrency=concurrency              Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input                          Данные для запуска скрипта
  --leaf=leaf                            Имя листа
  --max-resource-size=max-resource-size  [default: 104857600] Максимальный размер релизного артефакта
  --since=since                          SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:deploy`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:deploy

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:deploy:master`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:deploy:master

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:deploy:release`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:deploy:release

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:deploy:remove`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:deploy:remove

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:pulse:build`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:pulse:build

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:pulse:shooter`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:pulse:shooter

OPTIONS
  --concurrency=concurrency     Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU

  --enviroment=(trunk|release)  Окружение запуска (trunk, release), необходимо указывать для запусков в релизе или
                                транке

  --input=input                 Данные для запуска скрипта

  --leaf=leaf                   Имя листа

  --since=since                 SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:pulse:static`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:pulse:static

OPTIONS
  --concurrency=concurrency     Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU

  --enviroment=(trunk|release)  Окружение запуска (trunk, release), необходимо указывать для запусков в релизе или
                                транке

  --input=input                 Данные для запуска скрипта

  --leaf=leaf                   Имя листа

  --since=since                 SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:testpalm:suite`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:testpalm:suite

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:testpalm:synchronize`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:testpalm:synchronize

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:testpalm:synchronize:testing`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:testpalm:synchronize:testing

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:testpalm:validate`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:testpalm:validate

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci ci:unit`

Запускает одноименный скрипт из package.json на каждом листе из фильтра

```
USAGE
  $ frontend-ci ci:unit

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci config NAME`

Вычисляет различные конфигурационные параметры на основе окружения

```
USAGE
  $ frontend-ci config NAME

ARGUMENTS
  NAME  (base|head|base-commit|base-hash|head-commit|branch-name|base-branch-name|release-service|release-service-path|r
        elease-service-version|release-service-prebuild-version|pr-number) Имя конфигурационного параметра
```

## `frontend-ci enable-skipped-tests`

Расскипывает тесты через testcop

```
USAGE
  $ frontend-ci enable-skipped-tests

OPTIONS
  --branchName=branchName  (required) Имя ветки
  --prNumber=prNumber      (required) Номер PR'а, по которому расскипываем тест
  --since=since            (required) SHA коммита, от которого вычисляется набор листьев для расскипывания тестов в них
```

## `frontend-ci expflags-sync`

Синхронизирует экспериментальные флаги с хранилищем флагов https://ab.yandex-team.ru/flag_storage/flag

```
USAGE
  $ frontend-ci expflags-sync

OPTIONS
  --action=update|upload  (required) upload или update
                          https://github.yandex-team.ru/search-interfaces/ci/tree/master/packages/expflags-cli#upload

  --since=since           (required) SHA коммита, от которого вычисляется набор листьев для синхронизации флагов в них
```

## `frontend-ci expflags-to-testids`

Запускает произвольный скрипт на каждом листе из фильтра

```
USAGE
  $ frontend-ci expflags-to-testids

OPTIONS
  --concurrency=concurrency      Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input                  Данные для запуска скрипта
  --leaf=leaf                    Имя листа
  --projectSuffix=projectSuffix  Суффикс, добавляемый через '-', к основному проекту, указанному в конфиге.
  --since=since                  SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci format-jobs-data`

Формирование данных по джобам для графовой оркестрации в CI

```
USAGE
  $ frontend-ci format-jobs-data

OPTIONS
  --since=since  (required) SHA коммита, от которого формируются данные по джобам
```

## `frontend-ci get-changes-in-workcopy`

Получает список затронутых файлов в рабочей копии и отправляет статистику в solomon. Используется в конвейере для анализа проверки immutable bootstrap

```
USAGE
  $ frontend-ci get-changes-in-workcopy
```

## `frontend-ci get-muted-checks`

Публикует в output список замьюченных проверок для frontend

```
USAGE
  $ frontend-ci get-muted-checks
```

## `frontend-ci help [COMMAND]`

display help for frontend-ci

```
USAGE
  $ frontend-ci help [COMMAND]

ARGUMENTS
  COMMAND  command to show help for

OPTIONS
  --all  see all commands in CLI
```

_See code: [@oclif/plugin-help](https://github.com/oclif/plugin-help/blob/v2.2.3/src/commands/help.ts)_

## `frontend-ci install-root`

Установка пакетов корня монорепозитория

```
USAGE
  $ frontend-ci install-root

OPTIONS
  --ci                          Использовать npm ci вместо npm i и добавить CI=true
  --ignore-cache                Игнорировать архив с node_modules
  --loglevel=loglevel           [default: error] Уровень логирования
  --prefer-no-install           По возможности использовать кэш без установки зависимостей
  --publish-node-modules-cache  Опубликовать архив с node_modules
```

## `frontend-ci internal:run-on-leaf`

Не пытайтесь вызывать эту команду!

```
USAGE
  $ frontend-ci internal:run-on-leaf

OPTIONS
  --args=args  (required)
  --job=job    (required)
```

## `frontend-ci leaves:fetch-modules`

Запускает произвольный скрипт на каждом листе из фильтра

```
USAGE
  $ frontend-ci leaves:fetch-modules

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci leaves:publish-modules`

Запускает произвольный скрипт на каждом листе из фильтра

```
USAGE
  $ frontend-ci leaves:publish-modules

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci pr-experiment`

Создаёт выборку и ссылку на залипание в шаблоны пулл-реквеста на продакшене.

```
USAGE
  $ frontend-ci pr-experiment

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --prNumber=prNumber        (required) Номер пулл-реквеста, для которого необходимо создать эксперимент
  --since=since              SHA коммита, от которого вычисляются измененные листья
```

## `frontend-ci publish-mq-artifacts`

Публикация ресурсов после влития в MQ,

```
USAGE
  $ frontend-ci publish-mq-artifacts

OPTIONS
  --concurrency=concurrency  Кол-во параллельных процессов. По умолчанию: кол-во ядер CPU
  --input=input              Данные для запуска скрипта
  --leaf=leaf                Имя листа
  --since=since              SHA коммита, от которого вычисляются измененные листья

DESCRIPTION
  чтобы не ждать выполнения джобы в транке и всегда получать максимально быстро актуальные артефакты в ПРе
```

## `frontend-ci workspace ACTION`

Позволяет работать с рабочим пространством используя overlayfs

```
USAGE
  $ frontend-ci workspace ACTION

ARGUMENTS
  ACTION  (attach|cache|unsquash) Выполняемое действие

OPTIONS
  -b, --baseHash=baseHash      SHA base-коммитов в PR'е
  -c, --headCommit=headCommit  SHA последнего коммита в PR'е
  -d, --dest=dest              Директория, в которую будут собраны исходники и патч
  -f, --filter=filter          Названия артефактов, которые нужно примонтировать (разделённые двоеточием)
  -p, --patch=patch            Директория c динамически обновляемым патчем
  -s, --src=src                Директории с исходными файлами (разделённые двоеточием)
  -w, --work=work              Вспомогательная рабочая директория. Нужна для работы overlayfs.
  --cmd=cmd                    Скрипт, который нужно выполнить в созданном рабочем пространстве
  --help                       show CLI help
```
<!-- commandsstop -->
