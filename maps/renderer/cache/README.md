# Maps-Core-Renderer-Cache

[[toc]]

## General information

Caching service for various basemap tiles (vmap, vmap2, vnav2, map, indoor) and their resources.
Essentially is just an nginx with large cache and [tilesgen](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/tilesgen), [tilesgen_osm](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/tilesgen_osm) as an upstreams.
Provides caching for maps.yandex.ru and mapkit tiles, reducing tilesgen load.
Aimed at ~90% cache average hit rate (may drop to 70-80% during sharp rps peak after new data release).

| Key | Value |
| --- | ----- |
| Call in case of obscurity | [Михаил Мартикайнен](https://staff.yandex-team.ru/martikainen), [Артем Козырев](https://staff.yandex-team.ru/grstray), [Ярослав Музыкантов](https://staff.yandex-team.ru/muzykantov)
| SRE | [Артем Козырев](https://staff.yandex-team.ru/grstray) |
| Sources | https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/cache |
| Service in ABC | https://abc.yandex-team.ru/services/maps-core-renderer-cache/ |
| CI (TestEnv) | https://beta-testenv.yandex-team.ru/project/maps_tests/job/BUILD_DOCKER_AND_RELEASE_MAPS_CORE_RENDERER_CACHE/history?limit=20 |

## URLs

Production
* `https://core-renderer-tiles.maps.yandex.net`
* `https://core-renderer-tiles-internal.maps.yandex.net`
* `https://core-renderer-tiles-osm.maps.yandex.net`
* `https://core-renderer-tiles-osm-internal.maps.yandex.net`

Testing
* `https://core-renderer-cache.common.testing.maps.yandex.net`
* `https://core-renderer-tiles-osm.common.testing.maps.yandex.net`

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks | Balancers |
| ------- | ------------- | -------------- | ----------------- |-----------|
| stable | [maps_core_renderer_cache_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_cache_stable/) | [core-renderer-cache.stable](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-cache-stable-panel-main/) | [maps_core_renderer_cache_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_cache_stable&view=tiles&limit=200) | [core-renderer-tiles.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-renderer-tiles.maps.yandex.net/show/)<br/>[core-renderer-tiles-internal.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-renderer-tiles-internal.maps.yandex.net/show/) |
| prestable | [maps_core_renderer_cache_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_cache_prestable/) | [core-renderer-cache.prestable](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-cache-prestable-panel-main/) | [maps_core_renderer_cache_prestable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_cache_prestable&view=tiles&limit=200) | --- |
| experiments | [maps_core_renderer_cache_experiments](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_cache_experiments/) | [core-renderer-cache.experiments](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-cache-experiments-panel-main/) | [maps_core_renderer_cache_experiments](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_cache_experiments&view=tiles&limit=200) | --- |
| testing | [maps_core_renderer_cache_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_cache_testing/) | [core-renderer-cache.testing](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-cache-testing-panel-main/) | [maps_core_renderer_cache_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_cache_testing&view=tiles&limit=200) | [core-renderer-cache.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list/core-renderer-cache.common.testing.maps.yandex.net_default/show/)<br/>[core-renderer-tiles-osm.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list/core-renderer-tiles-osm.common.testing.maps.yandex.net_default/show/) |

### Ratelimiter panels
[maps_core_renderer_cache](https://yasm.yandex-team.ru/template/panel/maps_core_renderer_cache-ratelimiter2-panel)

### Firewall macroses
| stagings | URL |
| ------- | --- |
| stable, prestable | [ \_MAPS_CORE_RENDERER_CACHE_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_RENDERER_TILESGEN_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_RENDERER_CACHE_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_RENDERER_TILESGEN_TESTING_RTC_NETS_ ) |

### Balancers

#### core-renderer-tiles.maps.yandex.net

desc | link
---|---
L3-L7 balancers in nanny (AWACS) | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-renderer-tiles.maps.yandex.net/show/
l3manager | https://l3.tt.yandex-team.ru/service/10099
racktables | https://racktables.yandex-team.ru/index.php?page=ipv4rspool&pool_id=15749
common metrics | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-renderer-tiles.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-renderer-tiles.maps.yandex.net;signal=service_total;
portoinst metrics | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-renderer-tiles.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-renderer-tiles.maps.yandex.net;
файрвол puncher | [core-renderer-tiles.maps.yandex.net](https://puncher.yandex-team.ru/?rules=exclude_rejected&sort=destination&values=all&systems=&destination=core-renderer-tiles.maps.yandex.net)

Balancer has hashing config:
```
    - cgi_hasher:
        parameters:
          - 'x'
          - 'y'
          - 'z'
        randomize_empty_match: true
    - balancer2:
        hashing:
          delay: '10s'
          steady: true
          request: 'GET /ping HTTP/1.1\nHost: core-renderer-cache.maps.yandex.net\r\n\r\n'
```

You can see incoming traffic in separated panels in [awacs monitoring panel](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-renderer-tiles.maps.yandex.net/monitoring/common): 

| Upstream  (Url to panel ) |
| --------------------------|
| [total](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-renderer-tiles.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-renderer-tiles.maps.yandex.net;signal=service_total) |
| [mobile](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-renderer-tiles.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-renderer-tiles.maps.yandex.net;signal=mobile) |
| [staticapi](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-renderer-tiles.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-renderer-tiles.maps.yandex.net;signal=staticapi) |
| [default/anonym/web-cleints](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-renderer-tiles.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-renderer-tiles.maps.yandex.net;signal=default) |

### SSL sertificates

[SECAUDIT-3893](https://st.yandex-team.ru/SECAUDIT-3893)

#### `core-renderer-tiles.maps.yandex.net`:
* [SECTASK-23200](https://st.yandex-team.ru/SECTASK-23200)
* [SECTASK-20438](https://st.yandex-team.ru/SECTASK-20438)
* [SECTASK-17933](https://st.yandex-team.ru/SECTASK-17933)

#### `*.core-renderer-tiles.maps.yandex.net`:
* [SECTASK-23744](https://st.yandex-team.ru/SECTASK-23744)
* [SECTASK-20446](https://st.yandex-team.ru/SECTASK-20446)

#### `core-renderer-tiles-osm.maps.yandex.net`:
* [SECTASK-34303](https://st.yandex-team.ru/SECTASK-34303)

### What happens when service is down

If not operating properly, certain visible effect may arise:
* partial or complete absence of map tiles in mapkit or maps.yandex.ru
* wrong or corrupted map tiles in mapkit or maps.yandex.ru

### What can go wrong

#### Cache is corrupted/wrong or (almost) no memory left:
To clean cache you can change pod state (ACTIVE -> PRESENT -> ACTIVE) or manualy clean cache: `supervisorctl stop nginx`, `rm -rf /tmpfs/nginx_cache/vec_rdr/*`, `supervisorctl start nginx`.

#### Many 5xx/4xx
Check backend service [maps_core_renderer_tilesgen](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/tilesgen/readme.md)

### How to deploy new version

1. Docker image will be built in TestEnv task [BUILD_DOCKER_AND_RELEASE_MAPS_CORE_RENDERER_CACHE](https://beta-testenv.yandex-team.ru/project/maps_tests/job/BUILD_DOCKER_AND_RELEASE_MAPS_CORE_RENDERER_CACHE/history) after a commit to [maps/renderer/cache](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/cache).
2. The new image will be automatically released to [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_cache_testing/).
3. Check manually that bugs are fixed.
4. Deploy to prestable: call `maps/renderer/cache$ ya tool sedem release start .`
5. Wait for a successful prestable deployment (approximately 15-20 min).
6. Check service monitorings for the next 24 hours. Look at [prestable panel](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-cache-prestable-panel-main)
7. Deploy to stable: check tag version in output of `maps/renderer/cache$ ya tool sedem release info .` and call `maps/renderer/cache$ ya tool sedem release step . TAG_VERSION stable`
8. Wait for a successful stable deployment (approximately 2 hour).
9. Check service monitorings and have fun.

## Known clients

* [mobile proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy/README.md)
* [staticapi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/staticapi/README.md)
* [mobile printer: part of staticapi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/staticapi/README.md)
* [legacy mobile mapsnavi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/legacy/mapsnavi/readme.md)

## Backend services

* [maps-core-renderer-tilesgen](https://abc.yandex-team.ru/services/maps-core-renderer-tilesgen/) ([readme](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/tilesgen/readme.md)) is used to load tiles and its resource
* [maps-core-renderer-tilesgen-osm](https://abc.yandex-team.ru/services/maps-core-renderer-tilesgen-osm/) ([readme](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/tilesgen_osm/README.md)) is used to load OSM tiles and its resource

## SLA
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_renderer_cache)
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_renderer_cache.py)

## Logs

Look for file logs inside containers in Nanny services

| Name | URL/path |
| ---- | -------- |
| nginx | `/var/log/nginx/access-tskv.log`,`/var/log/nginx/error.log` |
| roquefort | `/var/log/yandex/maps/roquefort` |
| supervisord | `/var/log/supervisor` |
| syslog (unfiltered) | `/var/log/syslog` |
| cron | `/var/log/cron.log` |

## Logs in [YT](https://yql.yandex-team.ru):

```
USE hahn;
SELECT *
--FROM RANGE(`//logs/maps-log/stream/5min`, `2021-07-22T14:20:00`, `2021-07-22T14:45:00`)
FROM RANGE(`//logs/maps-log/1d`, `2021-07-22`, `2021-07-22`)
WHERE vhost = 'core-renderer-cache.maps.yandex.net'
   OR vhost = 'core-renderer-tiles.maps.yandex.net'
   OR vhost = 'core-renderer-tiles-osm.maps.yandex.net'
LIMIT 1000
```
