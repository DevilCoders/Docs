# metrostroy
Administrative interface for controlling the content for Yandex.Metro

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-metrostroy/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-metrostroy |

## Instances

| Environment | URL |
|---|---|
| Testing | https://metrostroy.tst.c.maps.yandex-team.ru |
| Production | https://metrostroy.c.maps.yandex-team.ru |

## Storage

 * MDS S3 bucket: `metrokit-bundles`
 * MDB cluster name: [maps_front_metrostroy_production](https://yc.yandex-team.ru/folders/fooogbp3i1ts5p2na6o0/managed-postgresql/cluster/daafc2dd-1348-45ae-a9c3-d372d6a5f58e)

## Documentation

N/A

## Known clients

N/A

## What happens when service is down

The content for Yandex.Metro will not be editable.

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

| Name | URL |
|---|---|
| Golovan |  https://yasm.yandex-team.ru/template/alert/maps-front-metrostroy-production-app |
| Juggler |  https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-metrostroy_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-metrostroy_production |

## Balancer

| Name | URL |
|---|---|
| Porto metrics | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-metrostroy.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-metrostroy.slb.maps.yandex.net/ |
| Requests | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-metrostroy.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-metrostroy.slb.maps.yandex.net/ |

## Logs

| Name | URL/path |
|---|---|
| App | `https://deploy.yandex-team.ru/stage/maps-front-metrostroy_production/logs` |
| Juggler Client, Push client | `/var/log/supervisor/` |
| Nginx | `/var/log/nginx/access.log` |

If you need to read logs from instance, then you need:

1. Go to your stage and copy the SSH command to connect to the box: `ssh -6 root@<IPv6>`.
2. Run `logs stdout` (or `stderr`, `nginx`).

## Vault

- [maps-front-metrostroy.production.app](https://yav.yandex-team.ru/secret/sec-01ect06z1n852pd2xdxwnavnw3/explore/versions)
- [maps-front-metrostroy.testing.app](https://yav.yandex-team.ru/secret/sec-01ecsz662wncy8qzmqcgth5s9g/explore/versions)

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
