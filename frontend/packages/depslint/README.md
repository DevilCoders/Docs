depslint
=====
Утилита для фиксации версий зависимостей в монорепозитории.
Проверяет зависимоcти перечисленных файлов `package.json` на соответствие зафиксированным версиям. Версии фиксируются с помощью конфигурационного файла.

<!-- toc -->
* [Example](#example)
* [Usage](#usage)
* [Options](#options)
* [Configure](#configure)
* [Commands](#commands)
<!-- tocstop -->

# Example
<img width="320" alt="depslint example" src="https://jing.yandex-team.ru/files/hatroman/2020-01-30_19-48-50.jpg">

# Usage
```sh-session
$ npm install -g @yandex-int/depslint
$ depslint lint
```

# Options
## --config, -c "{path}"
Путь до конфигурационного файла. По умолчанию `depslint` пытается загрузить `.depslint.json` из текущей директории.

# Configure
Конфигурационный файл.

Для внутренних пакетов монорепозитория можно указать в качестве версии `upstream`, в таком случае будет разрешена только последняя версия пакета, указанная в его package.json.
## Структура
### пример `.depslint.json`
```json
{
  "versions": {
    "actual": {
      "p1": "2.2.0",
      "p2": "12.1.7"
    },
    "outdated": {
      "p1": ["1.1.0", "1.1.1"]
    }
  },
  "restricted": {
    "p3": ["p4"]
  },
  "ignore": [
      "**/{dir1,dir2}/*"
  ]
}
```
### `packages`
Перечисляет все пакеты, для которых на уровне монорепозитория зафиксирована версия. В свойстве `approved` указана зафиксированная версия, в свойстве `allowedLegacy` перечислен список допустимых версий. См. [обновление версии пакета](#Обновление-версии-пакета).

### `ignore`
Массив `glob`-шаблонов. Здесь можно перечислить пакеты, в которых по каким-то причинам не нужно поддерживать актуальность версий. Например, пакеты разработка которых заморожена.

### `restricted`
Перечисляет пакеты, которые запрещено использовать в качестве новых зависимостей в листьях монорепозитория. В массиве перечислены пакеты, которые рекомендуются к использованию вместо запрещённых.

### Обновление версии пакета
По договоренности зафиксированная версия может измениться, в таком случае предыдущая зафиксированная версия попадает в `allowedLegacy` до момента переезда всех пакетов на новую `approved` версию. По оконании переезда эту версию следует удалить из `alloweLegacy`.

# Commands
<!-- commands -->
* [`depslint help [COMMAND]`](#depslint-help-command)
* [`depslint lint FILES`](#depslint-lint-files)

## `depslint help [COMMAND]`

display help for depslint

```
USAGE
  $ depslint help [COMMAND]

ARGUMENTS
  COMMAND  command to show help for

OPTIONS
  --all  see all commands in CLI
```

_See code: [@oclif/plugin-help](https://github.com/oclif/plugin-help/blob/v2.2.3/src/commands/help.ts)_

## `depslint lint FILES`

Проверяет консистентность зависимостей в указанных файлах.

```
USAGE
  $ depslint lint FILES

OPTIONS
  -c, --config=config     [default: .depslint.json] путь до файла с конфигом
  --bail                  выставлять exit code 1, если хотя бы 1 пакет содержит неверные зависимости
  --with-checkout-config  Использовать checkoutConfig для получения baseCommit

EXAMPLES
  $ depslint lint path/to/package.json another/package.json
  $ depslint lint path/to/package.json another/package.json --with-checkout-config
  $ depslint lint --help
```
<!-- commandsstop -->
