# Static Maps API

You can use the Static API to get an image of part of the map and show it on a website or in an app.

The Static API returns an image of the map in response to an HTTPS request. You can append parameters and values to the URL in order to set the map center, size, and viewport, add placemarks, and show traffic. Data is updated for each request, so the map is always current.

**Table of Contents**
[[toc]]

## General information

| Name | Link |
| ---- | ---- |
| ABC Service | [Static Maps API](https://abc.yandex-team.ru/services/maps-core-renderer-staticapi/) |
| Maintainers | [Yaroslav Muzykantov](https://staff.yandex-team.ru/muzykantov), [Artem Kozyrev](https://staff.yandex-team.ru/grstray), [Michael Martikainen](https://staff.yandex-team.ru/martikainen) |
| SRE | [Yaroslav Muzykantov](https://staff.yandex-team.ru/muzykantov) |
| Tracker queue | [MAPSPRINTER](https://st.yandex-team.ru/MAPSPRINTER) |
| Source code (arcadia) | [maps/renderer/staticapi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/staticapi) |
| Post-commit docker image build | [BUILD_DOCKER_AND_RELEASE_MAPS_CORE_RENDERER_STATICAPI](https://beta-testenv.yandex-team.ru/project/maps_tests/job/BUILD_DOCKER_AND_RELEASE_MAPS_CORE_RENDERER_STATICAPI/history) |
| Dashboard (nanny services) | [maps_core_renderer_staticapi](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_renderer_staticapi/) |
| Load testing (lunapark) | [regress/MAPSRENDER/maps-core-renderer-staticapi](https://lunapark.yandex-team.ru/regress/MAPSRENDER?service=maps-core-renderer-staticapi), task: [MAPSRENDER-2355](https://st.yandex-team.ru/MAPSRENDER-2355) |
| SLA (stat report) | [maps_core_renderer_staticapi](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_renderer_staticapi) |

## URLs

Production
* `https://static-maps.yandex.ru`
* `https://enterprise.static-maps.yandex.ru` (CNAME `static-maps.yandex.ru`)
* `https://yandex.{tld}/maps-api-static`

Testing
* `https://core-renderer-staticapi.common.testing.maps.yandex.net`
* `https://core-renderer-staticapi-enterprise.common.testing.maps.yandex.net`
* `https://l7test.yandex.ru/maps-api-static`

Testing legacy (see [MAPSPRINTER-99](https://st.yandex-team.ru/MAPSPRINTER-99)): 
* `https://static-maps.tst.maps.yandex.ru` (CNAME `core-renderer-staticapi.testing.maps.yandex.net`)
* `https://enterprise.static-maps.tst.maps.yandex.ru` (CNAME `core-renderer-staticapi.testing.maps.yandex.net`)
* `https://core-renderer-staticapi.testing.maps.yandex.net`

Development (internal urls, don't use in other projects)
* `https://core-renderer-staticapi.maps.yandex.net`
* `https://core-renderer-staticapi-prestable.maps.n.yandex.ru`
* `https://core-renderer-staticapi-unstable.maps.n.yandex.ru`

## Known clients

* SERP
* Alice: route card, weather card
* Yandex.Taxi, Uber
* Yandex.Districts
* external web sites
* external apps
* mobile apps with old MapKit

## What happens when service is down

### The whole service is unavailable

* Static Maps wizard on SERP stops to be loaded. User will see a gray rectangle instead of the map image.
* Alice will not be able to load route image and map layer for weather card.
* Map images stops to be loaded on external web sites.
* External apps will not be able to load map images.

### Partial degradation

This service depends on several backend services. When one of the backend services is unavailable, response timings will grow and this service might respond with 500 HTTP status code to a fraction of requests.
* If _apikeys_ is unavailable, all enterprise requests will be accepted.
* If _maps-core-keyserv_ is unavailable, all non-enterprise requests with a key will be accepted without restrictions.
* If _maps-core-meta_ is unavailable, this service will respond with 500 HTTP status code when meta information for requested area of the map is missing in the cache.
* If one of _maps-core-renderer-cache_, _maps-core-jams-rdr_ or _maps-core-sat_ is unavailable, this service will respond with 500 HTTP status code to requests for map/skl, trf or sat layers, respectively.

## Backend services

* [apikeys](https://abc.yandex-team.ru/services/userapikeys/) ([wiki](https://wiki.yandex-team.ru/tech/developer/)) is used to validate keys for enterprise requests from external clients.
* [maps-core-keyserv](https://abc.yandex-team.ru/services/maps-core-keyserv/) ([readme](https://a.yandex-team.ru/arc/trunk/arcadia/maps/fastcgi/keyserv/README.md)) is used to validate keys for requests from internal clients: SERP, Alice, Yandex.Taxi, Uber.
* [maps-core-meta](https://abc.yandex-team.ru/services/maps-core-meta/) ([readme](https://a.yandex-team.ru/arc/trunk/arcadia/maps/fastcgi/meta/README.md)) is used to get available zooms and tiles versions.
* [maps-core-renderer-cache](https://abc.yandex-team.ru/services/maps-core-renderer-cache/) ([readme](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/cache/README.md)) is used to load map tiles.
* [maps-core-jams-rdr-cache](https://abc.yandex-team.ru/services/maps-core-jams-rdr-cache/) ([readme](https://a.yandex-team.ru/arc/trunk/arcadia/maps/jams/renderer2/cache/README.md)), [maps-core-jams-rdr](https://abc.yandex-team.ru/services/maps-core-jams-rdr/) ([readme](https://a.yandex-team.ru/arc/trunk/arcadia/maps/jams/renderer2/realtime/README.md)) is used to load traffic jam tiles.
* [maps-core-sat](https://abc.yandex-team.ru/services/maps-core-sat/) ([readme](https://a.yandex-team.ru/arc/trunk/arcadia/maps/factory/satproxy/README.md)) is used to load satellite tiles.

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks | Balancers |
| ------- | ------------- | -------------- | ----------------- | --------- |
| stable | [maps_core_renderer_staticapi_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_staticapi_stable/) | [core-renderer-staticapi.stable](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-staticapi-stable-panel-main/) | [maps_core_renderer_staticapi_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_staticapi_stable&view=tiles&limit=200)<br>[maps_core_renderer_staticapi_quota_stable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_staticapi_quota_stable&view=tiles&limit=200) | [static-maps.yandex.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-renderer-staticapi.maps.yandex.net/show/)<br>[yandex.{tld}/maps-api-static](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast/upstreams/list/maps-api-static/show/ "knoss_fast/maps-api-static") |
| prestable | [maps_core_renderer_staticapi_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_staticapi_prestable/) | [core-renderer-staticapi.prestable](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-staticapi-prestable-panel-main/) | [maps_core_renderer_staticapi_prestable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_staticapi_prestable&view=tiles&limit=200) | [core-renderer-staticapi-prestable.maps.n.yandex.ru](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-renderer-staticapi-prestable-slb) |
| testing | [maps_core_renderer_staticapi_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_staticapi_testing/) | [core-renderer-staticapi.testing](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-staticapi-testing-panel-main/) | [maps_core_renderer_staticapi_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_staticapi_testing&view=tiles&limit=200)<br>[maps_core_renderer_staticapi_quota_testing](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_staticapi_quota_testing&view=tiles&limit=200) | [core-renderer-staticapi.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list/core-renderer-staticapi.common.testing.maps.yandex.net_default/show/)<br>[core-renderer-staticapi-enterprise.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list/core-renderer-staticapi-enterprise.common.testing.maps.yandex.net_default/show/)<br>[l7test.yandex.ru/maps-api-static](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast_testing/upstreams/list/maps-api-static/show/)<br>[static-maps.tst.maps.yandex.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-renderer-staticapi.testing.maps.yandex.net/show/) |
| regression | [maps_core_renderer_staticapi_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_staticapi_load/) | [core-renderer-staticapi.load](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-staticapi-load-panel-main/) | [maps_core_renderer_staticapi_load](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_staticapi_load&view=tiles&limit=200) | |
| manual experiments | [maps_core_renderer_staticapi_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_staticapi_unstable/) | [core-renderer-staticapi.unstable](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-staticapi-unstable-panel-main/) | [maps_core_renderer_staticapi_unstable](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_staticapi_unstable&view=tiles&limit=200) | [core-renderer-staticapi-unstable.maps.n.yandex.ru](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-renderer-staticapi-unstable-slb) |

[all stagings monitorings (tag=maps_renderer_staticapi)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dmaps_renderer_staticapi&view=tiles&statuses=WARN%2CCRIT&limit=200)

### Ratelimiter panel

[maps_core_renderer_staticapi](https://yasm.yandex-team.ru/template/panel/maps_core_renderer_staticapi-ratelimiter2-panel) (WARN: rps is weighted and [multiplied by 10](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/staticapi/lua/staticapi_rate_limiter_weight.lua?rev=r7985742#L1))

### Logs

Backends:
- `unified_agent select -s staticapi -f`
- `unified_agent select -s nginx -f`

To list all available storages call `unified_agent select -l`.

See also [unified_agent select --help](https://docs.yandex-team.ru/unified_agent/operations/#select-command).

YT:
```
use hahn;
select *
from `logs/maps-log/1d/2021-02-28`
-- from range(`logs/maps-log/1d`)            -- last 90 days
-- from range(`logs/maps-log/stream/5min`)   -- today
where tskv_format = 'staticapi'
and (vhost like 'static-maps.yandex.ru%' or  -- may be static-maps.yandex.ru:443
     vhost like 'enterprise.static-maps.yandex.ru%' or
     vhost like 'yandex.%')
and (request like '/1.x%' or request like '/maps-api-static/1.x%')
and (status like '2%' or status like '3%' or status like '429')
```

YT examples:
- [query most popular sizes](https://yql.yandex-team.ru/Operations/YE5sbguEIxfYAGCTsoeLjX-bSS0Q_ervJZPyxjqjKNU=)
- [query most popular layers](https://yql.yandex-team.ru/Operations/YE5stQPTTsvpBgb52w-7QswN6HWoV1frBrelmn1SKuM=)

Balancers:
- `/logs/current-access_log-balancer-443`
- `/logs/current-access_log-balancer-80`

### Accesses

* [core-renderer-staticapi.maps.yandex.net](https://puncher.yandex-team.ru/?destination=core-renderer-staticapi.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination)
* [core-renderer-staticapi.testing.maps.yandex.net](https://puncher.yandex-team.ru/?destination=core-renderer-staticapi.testing.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination)
* [\_MAPS_CORE_RENDERER_STATICAPI_STABLE_RTC_NETS\_](https://puncher.yandex-team.ru/?source=_MAPS_CORE_RENDERER_STATICAPI_STABLE_RTC_NETS_&rules=exclude_rejected&values=all&sort=source)
* [\_MAPS_CORE_RENDERER_STATICAPI_TESTING_RTC_NETS\_](https://puncher.yandex-team.ru/?source=_MAPS_CORE_RENDERER_STATICAPI_TESTING_RTC_NETS_&rules=exclude_rejected&values=all&sort=source)

### How to deploy new version

1. Docker image will be built in TestEnv task [BUILD_DOCKER_AND_RELEASE_MAPS_CORE_RENDERER_STATICAPI](https://beta-testenv.yandex-team.ru/project/maps_renderer/job/BUILD_DOCKER_AND_RELEASE_MAPS_CORE_RENDERER_STATICAPI/history) after a commit to [maps/renderer/staticapi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/staticapi).
2. The new image will be automatically released to _testing_, _load_ and _unstable_ services.
3. Check manually that bugs are fixed and new features are available in testing. Check regression.
4. Call `maps/renderer/staticapi$ ya tool sedem release start .` to release to _prestable_.
5. Wait for a successful prestable deployment. Check service monitorings for the next 24 hours.
6. Call `maps/renderer/staticapi$ ya tool sedem release info .` to check release version.
7. Call `maps/renderer/staticapi$ ya tool sedem release step . VERSION stable` to release to _stable_.
8. Check service monitorings and have fun.

## External configs

* Ratelimiter: [maps_core_renderer_staticapi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_renderer_staticapi)
* TestEnv: [BuildDockerAndRelease.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/maps/BuildDockerAndRelease.yaml) (_MAPS_CORE_RENDERER_STATICAPI)
* SLA calculator: [maps_core_renderer_staticapi.py](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_renderer_staticapi.py)
* Mobile proxy, legacy layers nvmap, nvsatskl: [layers.service.conf](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy/config/mapkit2/locations/layers.service.conf?rev=5515789#L58)
* Legacy mobile proxy: [mobile-printer.conf](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/legacy/mapkit/docker/install/etc/template_generator/templates/etc/fastcgi2/available/mobile-printer.conf?rev=5535817#L42)

## API keys

Clients keys and secrets are stored in YaVault: https://yav.yandex-team.ru/?tags=maps-staticapi-apikey

To create new account:
1. Generate api_key and secret:
  * `$ python3 -c 'import uuid; print(uuid.uuid4())'`
  * `$ python3 -c 'import secrets; print(secrets.token_urlsafe(30))'`
2. Create new secret in YaVault using as example an [existent secret](https://yav.yandex-team.ru/?tags=maps-staticapi-apikey).
3. Add the new api_key to the [ratelimiter config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_renderer_staticapi/stable.yaml).
4. Add a signed URL with the new api_key to [staticapi_visual_tests.html](staticapi_visual_tests.html). Use [maps/infra/apiteka/signature/url-signer.html](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/apiteka/signature/url-signer.html) to make URL signature.
5. Add the secret version to the [SEDEM config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/staticapi/sedem_config/secrets.yaml) (use [tools/import-credentials](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/staticapi/tools/import-credentials)).
6. SEDEM will create new snapshots in prestable and stable. Manually activate them. Check prestable tests in [staticapi_visual_tests.html](staticapi_visual_tests.html).
7. Give to developers of client service:
  * the link to the secret in YaVault
  * the link to signature algorithm: https://wiki.yandex-team.ru/maps/dev/params/signature/
  * an example of signed URL with their api_key

New api_key and secret in YaVault can be created by the following command:
```
$ ya vault create secret \
    maps_staticapi_apikey_PROJECT \
    -c "PROJECT api_key and URL signing secret TASK-1234" \
    -r +reader:abc:PROJECT:scope:development \
    -r +reader:abc:maps-core-renderer-staticapi:scope:virtual \
    -r +owner:abc:maps-core-renderer-staticapi:scope:development \
    -r -owner:user:$(whoami) \
    -t maps-staticapi-apikey,stable \
    -k api_key=$(python3 -c 'import uuid; print(uuid.uuid4(), end="")') \
    -k signing_secret=$(python3 -c 'import secrets; print(secrets.token_urlsafe(30), end="")')
```

Legacy keys can be managed in https://keyserv.maps.yandex-team.ru (access granted for [abc:maps-front-keyserv-users](https://abc.yandex-team.ru/services/maps-front-keyserv/)).
Enterprise keys can be managed in https://admin-developer.tech.yandex-team.ru (access granted for IDM role [APIKeys/Менеджер Static API Карт](https://idm.yandex-team.ru/#rf-role=x0Zm0WBn#apikeys/staticmaps_manager;;;,rf-expanded=x0Zm0WBn,rf=1)).

## Links

* https://wiki.yandex-team.ru/maps/api/grid/
* https://wiki.yandex-team.ru/maps/dev/core/printer
* https://wiki.yandex-team.ru/maps/dev/core/layers/current.layers/
* https://wiki.yandex-team.ru/maps/api/enterprise/keys/#staticapi

## Fast test

Save locally and open [staticapi_visual_tests.html](staticapi_visual_tests.html) to check some test cases.
