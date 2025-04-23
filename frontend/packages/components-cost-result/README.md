components-cost-result
======================


<!-- toc -->
* [Usage](#usage)
* [Commands](#commands)
<!-- tocstop -->
# Usage
<!-- usage -->
```sh-session
$ npm install -g @yandex-int/components-cost-result
$ components-cost-result COMMAND
running command...
$ components-cost-result (-v|--version|version)
@yandex-int/components-cost-result/0.3.0 linux-x64 node-v12.18.1
$ components-cost-result --help [COMMAND]
USAGE
  $ components-cost-result COMMAND
...
```
<!-- usagestop -->
# Commands
<!-- commands -->
* [`components-cost-result help [COMMAND]`](#components-cost-result-help-command)
* [`components-cost-result send`](#components-cost-result-send)

## `components-cost-result help [COMMAND]`

display help for components-cost-result

```
USAGE
  $ components-cost-result help [COMMAND]

ARGUMENTS
  COMMAND  command to show help for

OPTIONS
  --all  see all commands in CLI
```

_See code: [@oclif/plugin-help](https://github.com/oclif/plugin-help/blob/v2.2.3/src/commands/help.ts)_

## `components-cost-result send`

Send the result of executing the reselective as a comment to the startrek ticket and add specific tag to ticket

```
USAGE
  $ components-cost-result send

OPTIONS
  -d, --date=date    publish version date
  -i, --input=input  components data
  -l, --lib=lib      library name
```

_See code: [src/commands/send/index.js](https://github.com/search-interfaces/frontend/blob/v0.3.0/src/commands/send/index.js)_
<!-- commandsstop -->
