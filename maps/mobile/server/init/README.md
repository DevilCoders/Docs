# Maps Core Mobile Init
1. Configures mapkit-based mobile applications with actual  mobile proxy url, experiments config.
2. Provides new clients with miid generator.

## General information
| Key | Value |
|---|---|
| Responsible developers | Dmitrij Fedin (dmfedin@yandex-team.ru) <br> Filipp Goltsov (trivias@yandex-team.ru) |
| Responsible SRE | Dmitrij Fedin (dmfedin@yandex-team.ru) <br> Filipp Goltsov (trivias@yandex-team.ru) |
| Sources | https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/init |
| ABC Service | https://abc.yandex-team.ru/services/maps-core-mobile-init/ |
| CI | https://a.yandex-team.ru/projects/maps-core-mobile-init/ci/actions/launches?dir=maps%2Fmobile%2Fserver%2Finit&id=build |

## Documentation
The service is based on [yacare base image](https://wiki.yandex-team.ru/maps/dev/core/yacare/).
The `mob_init` yacare service and its config (some of it is templated and depends on ecstatic-delivered data) is delivered in [pkg.json include section](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/init/docker/pkg.json)
Some additional software and data for config generation is delivered in [Dockerfile](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/init/docker/Dockerfile).

### Check-hooks
We have 2 types of check-hooks:
1. Default check-hooks, that checks servant availability, by requesting to /ping
2. Memory check-hooks. It controls available RAM, if there is less than 512mb, check-hook will fail and host will not release distributed lock

### Config structure
[maps/mobile/server/init/config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/init/config) contains config templates and non-templated configs. For templated configs, actual configs are generated using [maps/mobile/server/tools/layers_updater](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/tools/layers_updater) with ecstatic-delivered data.

### How to modify mob\_init yacare service
1. Make changes to source code at [maps/mobile/server/init](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/init).
2. Edit config templates and non-templated configs at [maps/mobile/server/init/config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/init/config)
3. Create a review, make sure somebody from [geoapps_infra group](https://a.yandex-team.ru/arc/trunk/arcadia/groups/geoapps_infra) ships it.
4. Commit your code.
5. After a commit to either maps/mobile/server/init or maps/mobile/server/init/config, TestEnv will trigger build automatically, new Docker image will be pushed to the maps/core-mobile-init repository.
6. We recommend to release using [Sedem Releases](https://wiki.yandex-team.ru/geo-infra/SEDEM/faq/#relizy).

**Important**: deploy your builds to *prestable* and *stable* only on Mondays—Thursdays, between 12:00 and 20:00 Moscow Time.

## Instances in Nanny
| Environment | URL |
|---|---|
| Stable | [maps_core_mobile_init_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_init_stable) |
| Prestable | [maps_core_mobile_init_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_init_prestable) |
| Datatesting | [maps_core_mobile_init_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_init_datatesting) |
| Datavalidation | [maps_core_mobile_init_datavalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_init_datavalidation) |
| Testing | [maps_core_mobile_init_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_init_testing) |
| Load | [maps_core_mobile_init_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_init_load) |

## Graphics dashboards
| Staging | Golovan panel |
|---|---|
| Stable+Prestable | [maps-core-mobile-init-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-init-stable-panel-main) |
| Prestable | [maps-core-mobile-init-prestable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-init-prestable-panel-main) |
| Datatesting | [maps-core-mobile-init-datatesting-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-init-datatesting-panel-main) |
| Datavalidation | [maps-core-mobile-init-datavalidation-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-init-datavalidation-panel-main) |
| Testing | [maps-core-mobile-init-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-init-testing-panel-main) |
| Load | [maps-core-mobile-init-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-init-load-panel-main) |

## Monitorings
| Type | URL |
|---|---|
| Juggler (All) | https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-mobile-init |
| Juggler (Stable) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_init_stable |
| Juggler (Prestable) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_init_prestable |
| Juggler (Datatesting) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_init_datatesting |
| Juggler (Datavalidation) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_init_datavalidation |
| Juggler (Testing) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_init_testing |
| Juggler (Load) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_init_load |

## Ratelimiter

Ratelimiter is enabled in mobile-init, but with [unlimited limit](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/mobile_init)
But requests are also limited on the mobile-http2-proxy with [finite limits on /config and /init](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_mobile/stable.yaml?rev=r8317775#L117-149)

## SLA
[Statface](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_mobile_init)

[maps_core_mobile_init.py config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_mobile_init.py).

## What happens when service is down

### GET config does not work
urls for mobile services are not delivered to mapkit. mapkit-based mobile apps do not work after restart.
Degradations:
When experiment backends experience errors or experiments do not work.

### GET miid does not work (handles: /miid, /random)
New clients are unable to receive config. See also [GET config does not work](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/init/README.md#get_config_does_not_work)
Clients are not able to get maps, nor build routes, nor use geo search, nor use any of maps mobile APIs.

## How to fix common problems
* Do experiments work? If experiments backend is broken, logs should show errors when querying `ab.yandex-team.ru/*` [Experiment admin duty calendar](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/calendar/)
* [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
* [The table of the responsible](https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/)
* Crit on `settings-load`? Probably you added new dataset for init. If it is, just add new dataset dir/name to `requiredServices` vector [here](https://a.yandex-team.ru/arc_vcs/maps/mobile/server/init/lib/settings_storage.cpp)

## Logs
| Name | URL/path |
|---|---|
| mob\_init yacare | /var/log/yandex/maps/mob\_init/* |
| Nginx | /var/log/nginx/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT | https://yql.yandex-team.ru<br> ```USE hahn; SELECT * FROM `logs/maps-log/1d/2019-09-28` WHERE vhost = 'core-mobile-init.maps.yandex.net';``` |

## Balancers

### Need to know
There is traffic mirroring from Stable+Prestable & Datatesting to Testing common balancer

| Staging | URL |
|---|---|
| Stable+Prestable & Datatesting| `core-mobile-init.maps.yandex.net` <https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-mobile-init.maps.yandex.net/show/> |
| Testing & Datavalidation | `core-mobile-init.testing.maps.yandex.net` <https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-mobile-init.testing.maps.yandex.net/show/> |
| Testing common | `core-mobile-init.common.testing.maps.yandex.net` <https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list/core-mobile-init.common.testing.maps.yandex.net_default/show> |

## Known clients
[Maps Core Mobile Proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/proxy/README.md)

## Ecstatic Datasets
* yandex-maps-coverage5-geoid
* yandex-maps-geodata5
* yandex-maps-mobile-driving-config-data
* yandex-maps-mobile-coverage-sat
* yandex-maps-mobile-coverage-vec
* yandex-maps-mobile-init-gdnc
* yandex-maps-mobile-init-streetview
* yandex-maps-mobile-init-trfl
* yandex-maps-mobile-init-indoor-radiomap
* yandex-maps-mobile-init-indoor-radiomap-coverage
* yandex-maps-renderer-blacklist-version
* yandex-maps-mobile-init-fonts
* yandex-maps-mobile-init-device-segments - [ scheduler stable ](https://sandbox.yandex-team.ru/scheduler/701368) - [ scheduler testing ](https://sandbox.yandex-team.ru/scheduler/700975) - [ source code ](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/sandbox/MapsMobilePublishDeviceSegments)

## Persistent Volumes
/persistent - a partition for persistent data storage (i.e. for data that needs to survive redeployments). All symlinks to it are ecstatic-related:
* /usr/share/yandex/maps/coverage5
* /usr/share/yandex/maps/mapkit/driving/2.x
* /usr/share/yandex/maps/mapkit/panoramas/2.x
* /var/cache/geobase
* /var/lib/yandex/maps/ecstatic
* /var/lib/yandex/maps/mobile/init

/logs - a persistent partition for logs. Symlink: /var/log

## Firewall macros
| staging | URL |
|---|---|
| Stable, Prestable, Datatesting | [ \_MAPS_CORE_MOBILE_INIT_STABLE_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MOBILE_INIT_STABLE_RTC_NETS_ ) |
| Testing, Load | [ \_MAPS_CORE_MOBILE_INIT_TESTING_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MOBILE_INIT_TESTING_RTC_NETS_ ) |
| Datavalidation | [ \_MAPS_CORE_MOBILE_INIT_DATAVALIDATION_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MOBILE_INIT_DATAVALIDATION_RTC_NETS_ ) |

## Regression Load Testing Configurations
| Type | URL |
|---|---|
| Without device id |
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSMOBCORE#Maps%20Core%20Mobile%20Init%20regression |
| Ammo | https://sandbox.yandex-team.ru/scheduler/17882 |
| CI | https://sandbox.yandex-team.ru/scheduler/17893 |
| With device id |
| Job | https://lunapark.yandex-team.ru/MAPSMOBCORE-14191 |
| Ammo | https://sandbox.yandex-team.ru/scheduler/701348 |
| CI | https://sandbox.yandex-team.ru/scheduler/701352 |

## Experiment Condition syntax
* `CONDITION:""` - empty condition
* `CONDITION:"[{"appVersion": {"minAppVersionAndroid": <version>, "maxAppVersionAndroid": <version>}}]"` - restriction by Android `<version>` (example `"7.0"`, `minAppVersionAndroid` must be less or equal `maxAppVersionAndroid`)
* `CONDITION:"[{"appVersion": {"minAppVersionIphone": <version>, "maxAppVersionIphone": <version>}}]"` - restriction by iOS `<version>` (example `"7.0"`, `minAppVersionIphone` must be less or equal `maxAppVersionIphone`)
* `CONDITION:"[{"anyDeviceSegments": [<segments>]}]"` - restriction by device `<segments>` (one or more segments, example `"with_2_gis", "driver"`)
* `CONDITION:"[{"appVersion": {"minAppVersionAndroid": <version>, "maxAppVersionAndroid": <version>}, "anyDeviceSegments": [<segments>]}]"` - combine restriction by `appVersion` and `anyDeviceSegments`
* `CONDITION:"[{"appVersion": {"minAppVersionAndroid": <version>, "maxAppVersionAndroid": <version>, "minAppVersionIphone": <version>, "maxAppVersionIphone": <version>}, "anyDeviceSegments": [<segments>]}]"` - all possible types restrictions in one condition
