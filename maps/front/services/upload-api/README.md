# upload-api
Proxy service for image uploads to `avatars-int.mds[t].yandex.net`.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-upload-api |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-upload-api |
| Balancer | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-upload-api.slb.maps.yandex.net/show/ |

## Instances

| Environment | URL |
|---|---|
| Testing | https://maps-upload-api.tst.c.maps.yandex.ru/ |
|| https://uralsib-admin.tst.c.maps.yandex-team.ru/ |
| Production | https://photo.upload.maps.yandex.ru/ |
|| https://photo.upload.maps.yandex.com/ |
|| https://photo.upload.maps.yandex.com.ge/ |
|| https://photo.upload.maps.yandex.uz/ |
|| https://photo.upload.maps.yandex.by/ |
|| https://photo.upload.maps.yandex.kz/ |
|| https://photo.upload.maps.yandex.kg/ |
|| https://photo.upload.maps.yandex.lv/ |
|| https://photo.upload.maps.yandex.lt/ |
|| https://photo.upload.maps.yandex.tj/ |
|| https://photo.upload.maps.yandex.tm/ |
|| https://photo.upload.maps.yandex.md/ |
|| https://photo.upload.maps.yandex.ee/ |
|| https://photo.upload.maps.yandex.fr/ |
|| https://photo.upload.maps.yandex.ua/ |
|| https://photo.upload.maps.yandex.com.tr/ |
|| https://photo.upload.c.maps.yandex-team.ru/ |

## Secrets

| Environment | Yav |
|---|---|
| Testing | [sec-01eg3gx4b9abs34n7byj11cpyc](https://yav.yandex-team.ru/secret/sec-01eg3gx4b9abs34n7byj11cpyc/) |
| Production | [sec-01eg3hd4pew3xzm15n6t9q4hcs](https://yav.yandex-team.ru/secret/sec-01eg3hd4pew3xzm15n6t9q4hcs/) |

## What happens when service is down
Image uploading in advertiser's personal account at `https://yandex.ru/maps/geoproduct/[id]` will stop working.

## SLA
99% requests are handled properly.

* Response http code not 5xx.

## Monitorings

### production
| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/?query=host%3Dmaps-front-upload-api_production.app |

## Dashboards
| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-upload-api_production/ |

### Balancer

| Name | URL |
|---|---|
| Porto metrics | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-upload-api.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-upload-api.slb.maps.yandex.net/ |
| Requests | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-upload-api.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-upload-api.slb.maps.yandex.net/ |

## Logs
| Name | URL/path |
|---|---|
| maps-logs | use [YQL](https://yql.yandex-team.ru/) to find `tskv_format == 'front-upload-api_app'`, [example](https://yql.yandex-team.ru/Operations/XTHDP59LnhPHXAMoqAloxr1gIcupZMKimPoIFa4J-NQ=) |
| application  | https://deploy.yandex-team.ru/stage/map-front-upload-api_production/logs |

## Regression Stress Testing Configurations
TBD

## Developing
Check out [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
