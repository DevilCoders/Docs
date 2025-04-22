#
#
#

l2 - control plane for load/dns. There is a set of instances
to make parallel shoot jobs. A set is defined in configuration
as folows:
```
# /etc/l2/l2.yaml
...
# configuration load/shoot instances
cluster:

  # ns+load type, testing set
  ns+load:
    man:
      - "alpha-26i.lxd.tt.yandex.net"
      - "dns-load01i.berry.yandex.net"
      - "dns-load02i.berry.yandex.net"
    sas:
      - "dns-load01h.berry.yandex.net"
    vla:
      - "dns-load01v.berry.yandex.net"
      - "build-bionic-01v.cdn.yandex.net"
...

```

Each instance has a running l2 daemon, listening on unix socket
for local client calls, and http 9883:
```
# /etc/l2/l2/yaml
...
l2:
  # d2 socket to listen (for monitoring,
  # controlling and statistics via http rest
  # api
  l2-socket: "/var/run/l2.socket"

  # l2 remote http port for control plane
  l2-port: 9883
```

```
alpha-26i.lxd:/etc/nginx/sites-enabled# systemctl status l2
● l2.service - L2 service
   Loaded: loaded (/lib/systemd/system/l2.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2020-04-08 23:52:19 MSK; 31min ago
  Process: 25519 ExecStartPre=/bin/chmod 755 /var/log/l2 (code=exited, status=0/SUCCESS)
  Process: 25518 ExecStartPre=/bin/chown syslog:adm /var/log/l2 (code=exited, status=0/SUCCESS)
  Process: 25517 ExecStartPre=/bin/mkdir -p /var/log/l2 (code=exited, status=0/SUCCESS)
 Main PID: 25520 (l2)
    Tasks: 9 (limit: 4915)
   CGroup: /system.slice/l2.service
           └─25520 l2: waiting for jobs

```

Shoot plan is implemented in yaml configuration for client call:
```
#
# l2 shoot example configuration
#
#shoot:
  # description of shoot, each run of shoot
  # is marked with uniq id for all instances
  description: "unbound:1.9.0/threads:54"

  # target to shoot, please check firewall/hbf
  # access/routing/etc
  target: "alpha-05i.lxd.tt.yandex.net:53"

  # type of ammo, could be ns1+ns2, ns3+ns4,
  # ns-cache, ns64-cache (used to select ammo file) 
  ammo: "ns-cache"

  # rps profile
  rps:
    duration: 30s
    type: "line"
    from: 5000
    to: 50000

  # workers per instance
  instances: 100

  # mode, could be sync/async
  mode: "sync"
```

As "fire" client command executed (1) shoot jobs are started on all
configured instances (2) client is waiting for the end of all instances
(3) initiates aggregate stage (4) pushes data into linapark
```
/usr/bin/l2 shoot fire --debug --file="/home/slayer/l2/l2.shoot-example.yaml"

```

Example output: https://paste.yandex-team.ru/991070


* schedule operations
    running schedules fire right-now with dry-run 
    on target "ns01e.name.yandex.net" 

    /usr/bin/l2 schedule fire --debug --dry-run --target="ns01e.name.yandex.net"
