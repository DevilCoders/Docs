uchenki-cli
=========

![](https://jing.yandex-team.ru/files/alexunix/uchenki-cli.png)
CLI Helper for load testing

* [Wiki](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/uchenki/#uchenkicli)<!-- toc -->
* [Installation](#installation)
* [Usage](#usage)
* [Commands](#commands)
<!-- tocstop -->

# Installation

### brew (macOS)
```sh-session
#[install]
brew tap marty/brew https://github.yandex-team.ru/Marty/brew
brew install uchenki-cli

#[upgrade]
brew update
brew upgrade uchenki-cli
```

### npm (Linux)
```sh-session
#[install]
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm -i -g uchenki-cli --registry="https://npm.yandex-team.ru"

#[upgrade]
sudo npm -i -g uchenki-cli --registry="https://npm.yandex-team.ru"
```

# Usage
<!-- usage -->
```sh-session
$ npm install -g uchenki-cli
$ uchenki COMMAND
running command...
$ uchenki (-v|--version|version)
uchenki-cli/0.0.10 darwin-x64 node-v14.10.1
$ uchenki --help [COMMAND]
USAGE
  $ uchenki COMMAND
...
```
<!-- usagestop -->
# Commands
<!-- commands -->
* [`uchenki autocomplete [SHELL]`](#uchenki-autocomplete-shell)
* [`uchenki conf [KEY] [VALUE]`](#uchenki-conf-key-value)
* [`uchenki help [COMMAND]`](#uchenki-help-command)
* [`uchenki l7load`](#uchenki-l7load)

## `uchenki autocomplete [SHELL]`

display autocomplete installation instructions

```
USAGE
  $ uchenki autocomplete [SHELL]

ARGUMENTS
  SHELL  shell type

OPTIONS
  -r, --refresh-cache  Refresh cache (ignores displaying instructions)

EXAMPLES
  $ uchenki autocomplete
  $ uchenki autocomplete bash
  $ uchenki autocomplete zsh
  $ uchenki autocomplete --refresh-cache
```

_See code: [@oclif/plugin-autocomplete](https://github.com/oclif/plugin-autocomplete/blob/v0.2.0/src/commands/autocomplete/index.ts)_

## `uchenki conf [KEY] [VALUE]`

manage configuration

```
USAGE
  $ uchenki conf [KEY] [VALUE]

ARGUMENTS
  KEY    key of the config
  VALUE  value of the config

OPTIONS
  -d, --cwd=cwd          config file location
  -d, --delete           delete?
  -h, --help             show CLI help
  -k, --key=key          key of the config
  -n, --name=name        config file name
  -p, --project=project  project name
  -v, --value=value      value of the config
```

_See code: [conf-cli](https://github.com/natzcam/conf-cli/blob/v0.1.9/src/commands/conf.ts)_

## `uchenki help [COMMAND]`

display help for uchenki

```
USAGE
  $ uchenki help [COMMAND]

ARGUMENTS
  COMMAND  command to show help for

OPTIONS
  --all  see all commands in CLI
```

_See code: [@oclif/plugin-help](https://github.com/oclif/plugin-help/blob/v3.2.0/src/commands/help.ts)_

## `uchenki l7load`

wrapper for l7heavy api

```
USAGE
  $ uchenki l7load

OPTIONS
  -h, --help                 show CLI help
  --dev                      use dev-nanny
  --oauth-token=oauth-token  provide token for nanny

DESCRIPTION
  Interactive load testing for multiple l7heavy balancers

EXAMPLE
  $ uchenki l7load
  ...
```
<!-- commandsstop -->
