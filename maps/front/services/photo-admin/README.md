# `Photoadmin`
`Back office for editing users photos`

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-photo-admin |
| YDeploy | https://deploy.yandex-team.ru/projects/maps-front-photo-admin |
| Tanker | https://tanker.yandex-team.ru/?project=ymaps-photoadmin&branch=master |

## Instances

| Environment | URL |
|---|---|
| Testing | https://photo-admin.tst.c.maps.yandex-team.ru |
| Production | https://photo-admin.maps.yandex-team.ru |

## What happens when service is down

Content managers are unable to moderate photos releases and remove photos from current photo layer in Yandex.Maps.

## Monitorings

| Name | URL |
|---|---|
| Yasm | https://yasm.yandex-team.ru/template/alert/maps-front-photo-admin-production-app |
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-photo-admin_production.app |

## Dashboards


| Name | URL |
|---|---|
| Yasm | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-photo-admin_production |

## Logs

| Name | URL/path |
|---|---|
| App | https://deploy.yandex-team.ru/stage/maps-front-photo-admin_production/logs |
| Juggler Client, Push client | `/var/log/supervisor` |
| Nginx | `/var/log/nginx/access.log` |

If you need to read logs from an instance, then you need:

1. Go to your stage and copy the SSH command to connect to the box: `ssh -6 root@<IPv6>`.
2. Run `logs stdout` (or `stderr`, `nginx`).

## Balancer

| Name | URL |
|---|---|
| Porto metrics | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-photo-admin.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-photo-admin.slb.maps.yandex.net/ |
| Requests | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-photo-admin.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-photo-admin.slb.maps.yandex.net/ |

## Vault

- [maps-front-photo-admin.production.app](https://yav.yandex-team.ru/secret/sec-01emkwrfp54f9st2nyyxtbdk6s/explore/versions)
- [maps-front-photo-admin.testing.app](https://yav.yandex-team.ru/secret/sec-01emkws3bekswatkrse3nbyhyv/explore/versions)

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
