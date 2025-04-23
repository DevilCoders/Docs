ownership-checker
=====

Утилита для проверки наличия владельцев пакета в `package.json` из [ABC](https://abc.yandex-team.ru/) или [Staff](https://staff.yandex-team.ru/)

# Commands
<!-- commands -->
* [`ownership-checker help [COMMAND]`](#ownership-checker-help-command)
* [`ownership-checker lint FILES`](#ownership-checker-lint-files)

## `ownership-checker help [COMMAND]`

display help for ownership-checker

```
USAGE
  $ ownership-checker help [COMMAND]

ARGUMENTS
  COMMAND  command to show help for

OPTIONS
  --all  see all commands in CLI
```

_See code: [@oclif/plugin-help](https://github.com/oclif/plugin-help/blob/v2.2.3/src/commands/help.ts)_

## `ownership-checker lint FILES`

Проверяет владельцев сервиса или пакета в package.json

```
USAGE
  $ ownership-checker lint FILES

OPTIONS
  --with-checkout-config  Использовать checkoutConfig для получения baseCommit

EXAMPLES
  $ ownership-checker lint --with-checkout-config path/to/package.json another/package.json
  $ ownership-checker lint path/to/package.json another/package.json
```
<!-- commandsstop -->
