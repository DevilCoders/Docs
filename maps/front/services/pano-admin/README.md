# Panoramas editor
The service allows to process raw panoramas from vendors and publish them in production.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-pano-admin/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-pano-admin |
| Tanker | https://tanker.yandex-team.ru/?project=ymaps-panoadmin&branch=master |

## Instances

| Environment | URL |
|---|---|
| Testing | https://pano-admin.tst.c.maps.yandex-team.ru |
| Production | https://pano-admin.yandex-team.ru |

## Known clients

The service is used by content managers.

## What happens when service is down

Content managers cannot process vendors panoramas.

## Monitorings

| Name | URL |
|---|---|
| Yasm | https://yasm.yandex-team.ru/template/alert/maps-front-pano-admin-production-app |
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-pano-admin_production.app |

## Dashboards

| Name | URL |
|---|---|
| Yasm | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-pano-admin_production |

## Logs

| Name | URL/path |
|---|---|
| App | https://deploy.yandex-team.ru/stage/maps-front-pano-admin_production/logs |
| Juggler Client, Push client | `/var/log/supervisor` |
| Nginx | `/var/log/nginx/access.log` |

If you need to read logs from an instance, then you need:

1. Go to your stage and copy the SSH command to connect to the box: `ssh -6 root@<IPv6>`.
2. Run `logs stdout` (or `stderr`, `nginx`).

## Balancer
| Name | URL |
|---|---|
| Porto metrics | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-pano-admin.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-pano-admin.slb.maps.yandex.net/ |
| Requests | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-pano-admin.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-pano-admin.slb.maps.yandex.net/ |

## Vault
- [maps-front-pano-admin.production.app](https://yav.yandex-team.ru/secret/sec-01ef1f4jmyfka15x8mkr6kwdny/explore/versions)
- [maps-front-pano-admin.testing.app](https://yav.yandex-team.ru/secret/sec-01ef1f5esp3a500zcw0sjb8m24/explore/versions)

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
