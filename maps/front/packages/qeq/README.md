# `qeq`

![version](https://badger.yandex-team.ru/npm/@yandex-int/qeq/version.svg)

Toolchain for DevOps.

## Prerequisites

* node >= 8

## Installation

```
npm install --registry http://npm.yandex-team.ru -g @yandex-int/qeq
```

Also you can turn on completion:

```sh
# Check you SHELL environment variable.
qeq install
```

More information about completion read in [`tabtab` documentation](https://github.com/mklabs/tabtab#1-install-completion).

## Update

```
npm install --registry http://npm.yandex-team.ru -g @yandex-int/qeq@latest
```


## Configuration

### Authorization

[Qtools authorization](https://github.yandex-team.ru/maps/qtools#authorization)

## Global options

* `--verbose` (`-v`) — enable verbose logging.
* `--log` (`-L`) — path to the log file.

## `exec`

```sh
qeq exec <objectId> [options] [-- command]
```

### Aliases

* `up` — Starts node process on selected instances.
* `down` — Stops node process on selected instances.

### `objectId`

The `objectId` consists of:
- YDeploy project: `yd:<stage>[.<deployUnit>[.<box>]]@datacenter`.
- Qloud project: `q:<project>[.<application>[.<environment>[.instance]]]@datacenter`.


Example of valid `objectId`:
```
q:maps.front-upload-api.test.app@man
    |         |           |   |   |
  project     |           |   |   |
         application      |   |   |
                   environment|   |
                              |   |
                        instance  |
                                  |
                              datacenter
```

Command example:
```
qeq exec maps.front-@myt --all -- "dpkg -l| grep geobase"
```

### `[options]`

```
  --verbose, -v  Enable verbose logging.              [boolean] [default: false]
  --all          Use wildcard for hosts matching      [boolean] [default: false]
  --cache, -c    Use saved cache for hosts fetching   [boolean] [default: true]
  --no-cache     Do not use saved cache for hosts fetching
```

### Examples

Example usage `--all` option:

```
qeq up maps.front-constructor-int
> error No matched environments

qeq up maps.front-constructor-int --all
> warn You're going to up 7 application(s) : +0ms
> warn maps.front-constructor-int.production.app.app-1 +1ms
> warn maps.front-constructor-int.production.app.app-2 +0ms
> warn maps.front-constructor-int.production.app.app-3 +0ms
> warn maps.front-constructor-int.stress.tank.tank-1 +0ms
> warn maps.front-constructor-int.stress.target.target-1 +0ms
> warn maps.front-constructor-int.testing.app.app-1 +0ms
> warn maps.front-constructor-int.testing.app.app-2 +0ms

qeq up maps.front-constructor-int.p --all
> warn You're going to up 3 application(s) : +0ms
> warn maps.front-constructor-int.production.app.app-1 +2ms
> warn maps.front-constructor-int.production.app.app-2 +0ms
> warn maps.front-constructor-int.production.app.app-3 +0ms
```

Command example:

```
qeq exec maps.front-@myt --all -- "dpkg -l | grep geobase"
```

## `distribute`

Copies a file from the local file system to the containers matched by the `objectId` expression. This util uses `exec`
for transport and inherits all of its flags. Currently the command can distribute a single text file per call.
Example:
```
qeq distribute yd:maps-front-discovery-int_production.app@man quick-hack.conf /etc/nginx/sites-enabled
```

## `drill`

Create issue in [tracker](https://st.yandex-team.ru/) and event in [infra](https://infra.yandex-team.ru/) by templates.

```sh
qeq drill
```

## `drill start`

Carry out maps front drill based on infra event.

```sh
qeq drill start https://infra.yandex-team.ru/event/337265
```

## `lsr`

Create LSR issue in [tracker](https://st.yandex-team.ru/MAPSLSR) and event in [infra](https://infra.yandex-team.ru/) by templates.

```sh
qeq lsr
```

## `mute`

Temporarily stop accident phone calls by setting juggler [mutes](https://docs.yandex-team.ru/juggler/notifications/mutes).

```sh
qeq mute
```

## `unmute`

Remove existing juggler [mutes](https://docs.yandex-team.ru/juggler/notifications/mutes).

```sh
qeq unmute
```

## `install`

Install completion to your environment.

## `uninstall`

Uninstall completion from your environment.

## `completion`

This command used by shell environment to get completion of your input.

## Troubleshooting

### `self signed certificate in certificate chain`

Install `yandex-internal-root-ca` and add `NODE_EXTRA_CA_CERTS` to your shell RC file (ex. `.bashrc`):
#### Linux:
```bashrc
export NODE_EXTRA_CA_CERTS=/usr/share/yandex-internal-root-ca/YandexInternalRootCA.crt
```
#### MacOS:
```
mkdir /usr/local/yandex-internal-root-ca
cd /usr/local/yandex-internal-root-ca
wget https://crls.yandex.net/YandexInternalRootCA.crt
export NODE_EXTRA_CA_CERTS=/usr/local/yandex-internal-root-ca/YandexInternalRootCA.crt
```
For check: ```printenv | grep NODE_EXTRA_CA_CERTS```

More info on [wiki](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vnode.js).

### `Host key verification failed`

Error example:

> The authenticity of host 'vla1-7a7bbd82b9fe.qloud-c.yandex.net (2a02:6b8:c0d:4e22:0:41e3:7a7b:bd82)' can't be established.
> RSA key fingerprint is SHA256:DrrdVoRSEoTlkBGH1yquAIuKSrAU6y+TsKNsQvihLQc.
> Are you sure you want to continue connecting (yes/no)?

Add `StrictHostKeyChecking no` to ssh configuration `~/.ssh/config`:

```
Host *.yandex.net
StrictHostKeyChecking no
```
