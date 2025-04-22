# `Quotateka`
`Backoffice for quota management system for Maps Platform APIs`

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-quotateka-admin/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-quotateka-admin/ |
| Tanker | https://tanker-beta.yandex-team.ru/project/maps-front-quotateka-admin/ |

## Instances

| Environment | URL |
|---|---|
| Testing | https://quotateka.tst.c.maps.yandex-team.ru/ |
| Production | https://quotateka.maps.yandex-team.ru/ |

## Balancer

| Environment | Namespace                                                                                                                              | Requests Stats                                                                                                                                                                                                                | Instance Stats                                                                                                                                                                                                   |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Production  | [front-quotateka-admin.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-quotateka-admin.slb.maps.yandex.net/show/)         | [Dashboard](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-quotateka-admin.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-quotateka-admin.slb.maps.yandex.net/)             | [Dashboard](https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-quotateka-admin.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-quotateka-admin.slb.maps.yandex.net/)         |

## Monitorings

| Type | URL |
|---|---|
| Yasm | https://yasm.yandex-team.ru/template/alert/maps-front-quotateka-admin-production-app |
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-quotateka-admin_production.app |


## Dashboards

| Name | URL |
|---|---|
| Yasm | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-quotateka-admin_production |

## Logs

| Name | URL/path | Example |
|---|---|---|
| App | https://deploy.yandex-team.ru/stage/maps-front-quotateka-admin_production/logs |[YQL](https://yql.yandex-team.ru/Operations/YGr7MNK3DKODbOlEW2uGkLfpFlOwm-Zi2Or9EJZnFQc=) |
| Juggler Client, Push client | `/var/log/supervisor` | |
| Nginx | `access-tskv.log` |[YQL](https://yql.yandex-team.ru/Operations/YGr7q794hqYIS4GL4crEgvD-s9D-TTac7nV3-4TzVZM=) |

If you need to read logs from an instance, then you need:

1. Go to your stage and copy the SSH command to connect to the box: `ssh -6 root@<IPv6>`.
2. Run `logs stdout` (or `stderr`, `nginx`).

## Vault

- [maps-front-quotateka-admin.production.app](https://yav.yandex-team.ru/secret/sec-01f21mrwsgt6f3n54h08da7gex/explore/versions)
- [maps-front-quotateka-admin.testing.app](https://yav.yandex-team.ru/secret/sec-01f21mrw2x51pdn1nd85q6xktc/explore/versions)


## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
