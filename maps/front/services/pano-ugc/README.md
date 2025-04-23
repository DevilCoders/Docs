# Yandex Panoramas
The service allows external vendors to upload panoramas to our backend.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-pano-ugc/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-pano-ugc |
| Tanker | https://tanker.yandex-team.ru/?project=pano-ugc&branch=master |

## Instances

| Environment | URL |
|---|---|
| Testing | https://pano.tst.c.maps.yandex.ru |
| Production | https://pano.maps.yandex.ru |

## Known clients

The service is used by external panoramas vendors.

## What happens when service is down

Panoramas vendors cannot upload panoramas to our backend.

## Monitorings

| Name | URL |
|---|---|
| Yasm | https://yasm.yandex-team.ru/template/alert/maps-front-pano-ugc-production-app |
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-pano-ugc_production.app |
| core-stv-ugc Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_stv_ugc_stable |

## Dashboards

| Name | URL |
|---|---|
| Yasm | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-pano-ugc_production |
| core-stv-ugc Yasm | https://yasm.yandex-team.ru/template/panel/maps-core-stv-ugc-stable-panel-main/ |

## Logs

| Name | URL/path |
|---|---|
| App | https://deploy.yandex-team.ru/stage/maps-front-pano-ugc_production/logs |
| Juggler Client, Push client | `/var/log/supervisor` |
| Nginx | `/var/log/nginx/access.log` |

If you need to read logs from an instance, then you need:

1. Go to your stage and copy the SSH command to connect to the box: `ssh -6 root@<IPv6>`.
2. Run `logs stdout` (or `stderr`, `nginx`).

## Balancer
| Name | URL |
|---|---|
| Porto metrics | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-pano-ugc.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-pano-ugc.slb.maps.yandex.net/ |
| Requests | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-pano-ugc.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-pano-ugc.slb.maps.yandex.net/ |

## Vault
- [maps-front-pano-ugc.production.app](https://yav.yandex-team.ru/secret/sec-01eex006v01qp6a41afa3rxzwq/explore/versions)
- [maps-front-pano-ugc.testing.app](https://yav.yandex-team.ru/secret/sec-01eewxs3v78qy7d6zc2sstfm8h/explore/versions)

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
