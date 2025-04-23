# MRC Tasks planner

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-mrc-planner/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-mrc-planner |
| Tanker | https://tanker.yandex-team.ru/?project=mrc-planner&branch=master |

## Instances

| Name | URL |
|---|---|
| Testing | https://mrc-planner.tst.c.maps.yandex-team.ru |
| Production | https://mrc-planner.maps.yandex-team.ru |

## What happens when service is down
If the service is down users are unable to publish or load any tasks-groups or exclusion-regions.

## Monitorings

| Name | URL |
|---|---|
| Yasm | https://yasm.yandex-team.ru/template/alert/maps-front-mrc-planner-production-app |
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-mrc-planner_production.app |

## Dashboards

| Name | URL |
|---|---|
| Yasm | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-mrc-planner_production/ |

## Logs
| Name | URL/path |
|---|---|
| App | https://deploy.yandex-team.ru/stage/maps-front-mrc-planner_production/logs |
| Juggler Client, Push client | `/var/log/supervisor/` |
| Nginx | `/var/log/nginx/access.log` |

If you need to read logs from an instance, then you need:

1. Go to your stage and copy the SSH command to connect to the box: `ssh -6 root@<IPv6>`.
2. Run `logs stdout` (or `stderr`, `nginx`).

## Balancer
| Name | URL |
|---|---|
| Porto metrics | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-mrc-planner.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-mrc-planner.slb.maps.yandex.net/ |
| Requests | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-mrc-planner.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-mrc-planner.slb.maps.yandex.net/ |

## Vault
- [maps-front-mrc-planner.production.app](https://yav.yandex-team.ru/secret/sec-01eg2z0rwa18h4j9qhvgeaj11z/explore/versions)
- [maps-front-mrc-planner.testing.app](https://yav.yandex-team.ru/secret/sec-01eg2yf5qbsjy3dn6jrca9t9p4/explore/versions)

## Documentation

[WORKFLOW.md](workflow.md)

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
