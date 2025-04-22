# HBF
Hostmanager need network connectivity to talk to
  * YP master servers
  * hm-server, hm-report

For every source network macro we need to request access to following entities.

## YP masters
Puncher rules:
  * YP L3 balancer access:
```
myt.yp.yandex.net
iva.yp.yandex.net
l3.man.yp.yandex.net
l3.sas.yp.yandex.net
l3.vla.yp.yandex.net
man-pre.yp.yandex.net
man.yp.yandex-team.ru
sas-test.yp.yandex.net
sas.yp.yandex-team.ru
xdc.yp.yandex.net
```

  * YP real server macro: `_YPMASTERSNETS_`
TCP, port: 8084

## hm-server
As we do not have separate macro and processes are running in *dom0* we need to request access to `_SEARCHPRODNETS_`.

TCP, port 8080, 8999


# Known sources
Hostmanager is running on hosts in several macros, so every time we add new server for it, we need to request
fw rules from:
  * `_SEARCHPRODNETS_` - RTC hosts
  * `_YTNETS_` - YT hosts
  * `_RTC_AMLNETS_` - anti-malware hosts
