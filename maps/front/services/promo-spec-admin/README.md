# `Админка спецпроектов`
Единое приложение для админок спецпроектов.

## Modules
### Админка спецпроектов Нави
Первая админка уже реализована. Это админка для заведения спецрекламы в Навигаторе. Она призвана автоматизировать ручное формирование спецрекламы описаное на [Wiki](https://wiki.yandex-team.ru/users/kydryashov/zavedenie-specproektov-na-s3/).   
Процесс публикации спецрекламы Навигатора описан на [Wiki](https://wiki.yandex-team.ru/ingradlanding/spisok-stranic/zavedenie-specproektov/).   
Новые админки будут создаваться в этом репозитории, если будет недостаточно функционала [Бункера](https://bunker.yandex-team.ru/maps-promo-specprojects).

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-promo-spec-admin/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-promo-spec-admin |
| IDM (testing) | https://idm.yandex-team.ru/system/maps-spec-admin-test/ |
| IDM (production) | https://idm.yandex-team.ru/system/maps-spec-admin/ |

## Instances

| Environment | URL |
|---|---|
| Testing | https://spec-admin.tst.c.maps.yandex-team.ru/ |
| Production | https://spec-admin.c.maps.yandex-team.ru/ |

## Storage

 * MDS S3 bucket: `spec-admin`
   Bucket info: `curl "https://s3-idm.mds.yandex.net/stats/buckets/spec-admin"`

## Instances

| Environment | URL |
|---|---|
| Testing | https://spec-admin.tst.c.maps.yandex-team.ru/navi/dashboard |
| Production | https://spec-admin.c.maps.yandex-team.ru/navi/dashboard |

## Known clients

* staff users
* IDM

## What happens when service is down

Менеджеры не смогут создавать спецпроекты.

## How to fix common problems

### Restart service
```
# supervisorctl restart node
```

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-promo-spec-admin_production.app |
| YASM | https://yasm.yandex-team.ru/template/alert/maps-front-promo-spec-admin-production-app |

## Dashboards

| Name | URL |
|---|---|
| YASM | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-promo-spec-admin_production |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/run/qloud/app.stdout /run/qloud/app.stderr` |
| Nginx | `/var/log/nginx` |
| Juggler Client, Push client | `/var/log/supervisor` |
| YT  | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-front-production-log& |

## Developing

Базовая информация [CONTRIBUTING.md](CONTRIBUTING.md)

После переезда почитать про спецпроекты и как их развернуть: [README.md](../../docs/spec-projects/README.md)
