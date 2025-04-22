@yandex-int/devkit
===================

<!-- description -->
Инструменты для рефакторинга и написания компонентов. Definitely not bem-tools!
<!-- descriptionstop -->

[![oclif](https://img.shields.io/badge/cli-oclif-brightgreen.svg)](https://oclif.io)
[![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/devkit)](https://oko.yandex-team.ru/pkg/@yandex-int/devkit)
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/packages/devkit&vcs=arc)](https://oko.yandex-team.ru/arc/frontend/packages/devkit)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=frontend/packages/devkit&vcs=arc)](https://oko.yandex-team.ru/arc/frontend/packages/devkit)

[![Version](https://img.shields.io/npm/v/@yandex-lego/devkit.svg)](https://npmjs.org/package/@yandex-lego/devkit)
[![License](https://img.shields.io/npm/l/@yandex-lego/devkit.svg)](https://a.yandex-team.ru/frontend/l/package.json)

<!-- toc -->
* [Usage](#usage)
* [Commands](#commands)
<!-- tocstop -->
# Usage
<!-- usage -->
```sh-session
$ npm install -g @yandex-int/devkit
$ dk COMMAND
running command...
$ dk (-v|--version|version)
@yandex-int/devkit/0.3.0 linux-x64 node-v12.18.1
$ dk --help [COMMAND]
USAGE
  $ dk COMMAND
...
```
<!-- usagestop -->
# Commands
<!-- commands -->
* [`dk health`](#dk-health)
* [`dk help [COMMAND]`](#dk-help-command)
* [`dk tun PORTS`](#dk-tun-ports)

## `dk health`

Проверка наличия доступов и других возможных проблем.

```
USAGE
  $ dk health

OPTIONS
  -h, --help  show CLI help

DESCRIPTION
  See:
  - https://doc.yandex-team.ru/si-infra/tunneler/access.html

EXAMPLE
  $ dk health
```

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

_See code: [@oclif/plugin-help](https://github.com/oclif/plugin-help/blob/v2.2.3/src/commands/help.ts)_

## `dk tun PORTS`

Open tunnels from remotely accessible host to local port with tunneler infrastructure. ![](./assets/how-it-works.png)

```
USAGE
  $ dk tun PORTS

ARGUMENTS
  PORTS  Local and optionally remote port or range for creating tunnel.
         Format: <localport>:<remoteport0>-<remoteport1>.
         <remoteport0> and <remoteport1> can be omitted.

OPTIONS
  -h, --help     show CLI help

  --realm=realm  [default: yandex.ru] Realm for creating accessible hostname.
                 Can be yandex (y), yandex-team (yt), or turbopages.org (t).

  --user=user    Login for creating accessible hostname (requires ssh-key).

EXAMPLES
  $ dk tun <ports..>
  $ dk tun 3000
  $ dk tun 3000:60000
  $ dk tun 3000:60000-60100
  $ dk tun 3000 3000
```
<!-- commandsstop -->
