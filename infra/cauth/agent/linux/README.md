# Linux CAuth
Modern cauth agent consists of yandex-cauth-userd daemon maintaining local authentication data cache
and nss_cauth_userd nss module. NSS module resolves users/groups communicating userd daemon via unix socket.

## Installation and configuration
Install `yandex-cauth-userd` package as follows:

    tee /etc/apt/sources.list.d/yandex-cauth.list <<EOF
    deb http://cauth.dist.yandex.ru/cauth stable/amd64/
    EOF

    export DEBIAN_FRONTEND=noninteractive
    apt-get update
    apt-get install yandex-cauth-userd

The package will replace legacy `yandex-cauth` package. In most cases no more configuration needed.

### Customization notice
yandex-cauth-userd provides ssh keys for sshd via unix socket through config option `AuthorizedKeysCommand` (configures in package postinstall script). This option should be set in cutomized sshd_config to

    AuthorizedKeysCommand /usr/bin/curl -s -X GET --unix-socket /run/yandex-cauth-userd.sock http://localhost/nss/v1/keys/%u

or system may become unaccessible via ssh.

### Config defaults
Actual configuration default could be always found at https://a.yandex-team.ru/arc/trunk/arcadia/infra/cauth/agent/linux/yandex-cauth-userd/internal/config/config.go


Full config example with defaults:
```
log:
    level: info
    output: stdout
repoConfig:
    keepVersions: 5  # How many versions of cache keep
    path: /var/cache/yandex-cauth-userd  # path to cache (avoid changing it mindlessly, it is used by symlinks in package)
cAuthConfig:
    url: https://cauth.yandex.net:4443  # cauth installation
    legacySources: ""  # /etc/cauth/cauth.conf sources field value (used if provided, otherwise userd tries to read it from /etc/cauth/cauth.conf)
daemonConfig:
    socketPath: /run/yandex-cauth-userd.sock  # path to listening socket (avoid changing it as it hardcoded in nss module)
    pidFile: /run/yandex-cauth-userd.pid
    enableSocketActivation: true  # set to false if running without systemd
    updateIntervalSec: 600
    updateRandomizedDelaySec: 600
    maxUpdatesPerMinute: 3  # throttling configuration
    updateHistoryFile: /run/yandex-cauth-userd-updates.json  # update history file
    resolveGroupMembers: true  # set to false for hosts with huge groups (dpt_yandex)
YASMConfig:
    pushEnabled: false
    ctype: unknown
    itype: unknown
    yasmURL: http://localhost:11005
    PushInterval: 5s
```
