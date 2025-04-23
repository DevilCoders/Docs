# Cartograph
## Graphic Yandex maps editor
Web service for create, read, view and share design of vector layer Yandex Maps.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-cartograph-admin/ |
| Qloud | https://platform.yandex-team.ru/projects/maps/front-cartograph-admin/ |

## Instances

| Environment | URL |
|---|---|
| Testing | https://cartograph.tst.c.maps.yandex-team.ru/ |
| Production | https://cartograph.maps.yandex-team.ru/ |

## Documentation

* [How to use a cartograph? The detailed guide for users.](https://doc.yandex-team.ru/ymaps/cartograph_usguide/)
* [Cartograph news in our team blog](https://clubs.at.yandex-team.ru/geodata-interfaces/)
* [Documentation for developers](docs/README.md)

## What happens when service is down
* Will block the designing of maps style. [Staff](https://staff.yandex-team.ru/departments/yandex_design_geo_maps/)

## Monitorings

### production
| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/?query=host%3Dmaps.front-cartograph-admin.production.app |

## Dashboards
| Name | URL |
|---|---|
| Main | [YASM](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps.front-cartograph-admin.production) |
| Porto metrics | [YASM](https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-cartograph-admin.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-cartograph-admin.slb.maps.yandex.net/) |
| Requests | [YASM](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-cartograph-admin.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-cartograph-admin.slb.maps.yandex.net/) |

## Logs
| Name | URL/path |
|---|---|
| NodeJS | /run/qloud/app.stdout |
| NodeJS | /run/qloud/app.stderr |
| Nginx | /var/log/nginx/error.log |
| Nginx | /var/log/nginx/access.log |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
