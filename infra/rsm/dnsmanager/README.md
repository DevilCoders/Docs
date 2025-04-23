# DNS Manager service

Use ((https://coredns.io coredns)) as library for running caching dns resolver. Run coredns with custom config and additional plugins.
All Yandex specific logic moved to plugins.
Before start coredns, dnsmanager reads the /etc/server_info.json for getting server location. And tring to get
in memory predefined config.
Each location based config file consist specific settings at least list of forwarders.


## Monitoring
* [Yasm Tree] (https://yasm.yandex-team.ru/menu/RTCSRE/DNS)
* [Yasm Chart Panel] (https://yasm.yandex-team.ru/template/panel/rtc_dns_new/)
* [Yasm Alert Panel] (https://yasm.yandex-team.ru/template/panel/rtc_dns_alerts_new)
* [Solomon] ()

## Corefile
Coredns based on ((https://caddyserver.com caddy server framework)) and of course
use configuration like in caddy. 
Short explonation described ((https://coredns.io/2017/07/23/corefile-explained/ here)) and ((https://coredns.io/manual/toc/#configuration here))
But if you want more understanding ((https://caddyserver.com/docs/caddyfile see original caddy documentation))

This file consists of one or more Server Blocks. Each Server Block lists one or more Plugins.
Those Plugins may be further configured with Directives.
Some plugins MUST defined once in Server Block this behave defined in source file for each plugin.
The order in which the plugins are executed is determined by
the ordering in arcadia/infra/rsm/dnsmanager/internal/libcoredns/plugin/plugin.go

### Test new config
Put new config with name coredns.conf to CONF_PATH and start
```
/usr/bin/dnsmanager coredns

```
By default CONF_PATH is /etc/yandex-dns-manager/libcoredns/

## Plugins
List of Yandex plugins:
* ((arcadia/infra/rsm/dnsmanager/internal/libcoredns/plugin/yasm/README.md yasm))
* ((arcadia/infra/rsm/dnsmanager/internal/libcoredns/plugin/staticfile/README.md staticfile))
* ((arcadia/infra/rsm/dnsmanager/internal/libcoredns/plugin/dummy/README.md dummy))

### Add new plugin
1) Read original how-to https://coredns.io/2017/03/01/how-to-add-plugins-to-coredns/
2) Put sources to arcadia/infra/rsm/dnsmanager/internal/libcoredns/plugin/
3) Define import in arcadia/infra/rsm/dnsmanager/internal/libcoredns/libcoredns.go
4) Define plugin in right place arcadia/infra/rsm/dnsmanager/internal/libcoredns/plugin/plugin.go
5) And don't forget to update internal/libcoredns/plugin/ya.make
