# `SPUTNICA`
`Service for management the orders of satellite mosaics`

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-sputnica/ |
| YDeploy | https://deploy.yandex-team.ru/projects/maps-front-sputnica |
| Tanker | https://tanker.yandex-team.ru/?project=ymaps-sputnica&branch=master |

## Instances

| Environment | URL |
|---|---|
| Testing | https://sputnica.tst.c.maps.yandex.ru/ |
| Production | https://sputnica.yandex.ru/ |

### L3 balancers

| Environment | Namespace | Requests Stats | Instance Stats |
|---|---|---|---|
| Production | [front-sputnica.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-sputnica.slb.maps.yandex.net/show/) | [Dashboard](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-sputnica.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-sputnica.slb.maps.yandex.net;) | [Dashboard](https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-sputnica.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-sputnica.slb.maps.yandex.net;) |

### Secrets

| Environment | URL |
|---|---|
| TVM Testing | https://yav.yandex-team.ru/secret/sec-01efp7vqrzwb07j2xt2pthgxev/explore/versions |
| TVM Production | https://yav.yandex-team.ru/secret/sec-01efp81s814m6mjrtbr4pjgwdj/explore/versions |


## What happens when service is down

`Контрагенты и картографы не смогут принимать спутниковые снимки`

## How to fix common problems

### Restart service
```
# supervisorctl restart node
```

### Change log level
0. ssh to the desired instance.
1. Open the config file `vim /usr/local/app/configs/production.yaml`.
2. Find the `logger` section.
3. Change the `level` property to one for the [supported ones](https://github.com/winstonjs/winston#logging-levels).
4. Restart the service.

**Note.** Do not forget to change the log level to the previous value, when you've finished debugging.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-sputnica_production.app |

## Dashboards

| Name | URL |
|---|---|
| YASM | https://yasm.yandex-team.ru/template/alert/maps-front-sputnica-production-app |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/run/qloud/app.stdout`, `/run/qloud/app.stderr` |
| Nginx | `/var/log/nginx/error.log`, `/var/log/nginx/access.log` |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
