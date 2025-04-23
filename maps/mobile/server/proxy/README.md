# Maps Core Mobile Proxy
A proxy for the overwhelming majority of mapkit requests.

## General information
| Key | Value |
|---|---|
| Responsible developers | Filipp Goltsov (trivias@yandex-team.ru) <br> Kirill Martynkov (kmartynkov@yandex-team.ru) <br> Dmitrij Fedin (dmfedin@yandex-team.ru)|
| Responsible SRE | Filipp Goltsov (trivias@yandex-team.ru) <br> Kirill Martynkov (kmartynkov@yandex-team.ru) <br> Dmitrij Fedin (dmfedin@yandex-team.ru)|
| Sources | https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy |
| ABC Service | https://abc.yandex-team.ru/services/maps-core-mobile/ |
| CI (TestEnv) | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_MOBILE_PROXY <br> https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_MOBILE_HTTP2 |

## Documentation
This proxy is based on [yacare base image](https://wiki.yandex-team.ru/maps/dev/core/yacare/).
Configs, http signature, and environment_linker are delivered in [pkg.json include section](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy/docker/pkg.json)
Some additional software is delivered in [Dockerfile](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy/docker/Dockerfile).

### How to release new proxy config
1. Edit nginx configs here: <https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy/config> and here: <https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy>.
2. Create a review, make sure somebody from [geoapps_infra group](https://a.yandex-team.ru/arc/trunk/arcadia/groups/geoapps_infra) ships it.
3. Commit your code.
4. Proceed to [Deploy instructions](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy#deploy-sedem-release)

### How to change certificate on proxy
1. Request [role](https://abc.yandex-team.ru/services/maps-core-mobile/?scope=cert).
2. Go to `Instance Spec` of the proxy and learn ID of current certificate.
3. Find certificate by ID at [Certificator](https://crt.yandex-team.ru/certificates).
4. Request to extend the certificate. New ticket will be created.
5. You will be asked to explain why you manage certificates manually. The explanation is: `maps-core-mobile-proxy`, `maps-core-mobile-http2` services are L7 balancers with additional features, they live right after L3 balancers. (Russian: Сервисы `maps-core-mobile-proxy`, `maps-core-mobile-http2` выполняют функцию L7-балансеров с дополнительной функциональностью, и живут сразу за L3-балансерами.).
6. Go to `Instance Spec`.
7. Click `Change` under old certificate.
8. Paste ID of new certificate and click `Save`.
9. Click `Save` near `Runtime`.
10. Click `Change` on current snapshot, `Active -> Apply`.
11. Remember the stagings order: do `testing` first, `prestable` second and eventually the `stable` one.

### How to modify software installations on the Docker image
1. `cd (Arcadia)/maps/mobile/server/proxy/spdy/docker` or `cd (Arcadia)/maps/mobile/server/proxy/http2/docker` or `cd (Arcadia)/maps/mobile/server/proxy/shared`

2.1. Edit `./pkg.json` to edit software delivered via [ya package](https://wiki.yandex-team.ru/yatool/package/)

2.2. Edit `./Dockerfile` (only in `spdy/docker` and `http2/docker`) to edit software delivered via apt-get.

2.3. If necessary, put/edit/remove scripts and configs in `./install` directory.

3. Create a review, make sure somebody from [geoapps_infra group](https://a.yandex-team.ru/arc/trunk/arcadia/groups/geoapps_infra) ships it.
4. Commit your code.
5. Proceed to [Deploy instructions](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy#deploy-sedem-release)

### Deploy (SEDEM release)

#### Important: do not forget to deploy to both SPDY and HTTP/2 proxies! Both of them have production load on them ATM, so version consistency is extremely important.

1. After a commit to either maps/mobile/server/proxy or maps/mobile/server/proxy/config, TestEnv will trigger build automatically, new Docker image will be pushed to the maps/core-mobile-proxy repository.
2. After a successful Docker image creation, navigate yourself to closest local Arcadia copy and checkout to freshest trunk. Change current directory to the desired proxy `sedem_config` location (either `maps/mobile/server/proxy/spdy` or `maps/mobile/server/proxy/http2`). You can also continue working from Arcadia root, in that case you need to replace `.` with the aforementioned paths in the following commands.
3. Type `ya tool sedem release info .` and check that your revision is in `Release candidates` table.
4. To deploy release candidate to testing, type `ya tool sedem release start . <index, e.g. @1>` and wait for completion.
5. On the previous step, SEDEM is supposed to print your version number. If this doesn't happen for some reason, you can extract it after release to testing with `ya tool sedem release info .` and take `Version` field value of testing/stress environment.
6. Make sure that everything works in testing.
7. To deploy to prestable/stable, use `ya tool sedem release step . <version number, e.g. 'V3.1'> <staging>`. Note: to proceed to the next release step (testing -> prestable, prestable -> stable), you will need to wait for about 1 day, otherwise SEDEM won't let you deploy. You need to have very serious reasons to deploy to stable right after prestable without waiting for 1 day to make sure everything works, but if you *really* want to override SEDEM deploy timeout, use `--force` flag.

Important: deploy your builds to prestable and stable only on Mondays—Thursdays, between 12:00 and 20:00 Moscow Time.

### How to create your own `maps_core_mobile_proxy_testing` service copy for development
1. [Go to Copy Service](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_proxy_testing/copy_service)
2. Change `Id` à la `(your username)_mobile_proxy_testing`. It has to end with `_testing` for environment_linker to link configs correctly.
3. Change ABC service to your service.
4. Check `Copy instances definition`.
5. Press `Submit`
6. In your new Nanny service, Go to Information: Tickets Integration and remove Docker release rule, so that new releases do not affect your service.
7. Allocate YP Pods. We recommend disk sizes the same as in the real testing proxy, so that logrotate does not overflow /logs volume. HDD suits development purpose, no need for an SSD. You might want to reduce CPU and RAM requirements. Use may use temporary junk quota for 2-4 weeks. With your ABC service owner consent, you may move the Pod set to the ABC service quota on this stage or later.
8. Go to Runtime: Instances, check the newly created YP Pod.
9. If you choose to use ecstatic on step 12, go to Runtime: Instance Spec: How to check container readiness, and remove Actions there.
10. Press Runtime: Save, Submit.
11. Change the created snapshot's state to Active.
12. Deliver /etc/yandex/maps/rate-limiter/config/access-config.json either [by copying the file from the real testing proxy](https://paste.yandex-team.ru/826762) or [by adding your service to ecstatic config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ecstatic/testing/yandex-maps-mobile-access-config.conf).

## Instances
| Environment |  SPDYS | HTTP/2 |
|---|---| ---|
| **Nanny dashboard** | [maps_core_mobile_proxy](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_mobile_proxy/) | [maps_core_mobile_http2](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_mobile_http2/) |
| Stable | [maps_core_mobile_proxy_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_proxy_stable) | [maps_core_mobile_http2_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_http2_stable) |
| Prestable | [maps_core_mobile_proxy_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_proxy_prestable) | [maps_core_mobile_http2__prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_http2_prestable) |
| Testing | [maps_core_mobile_proxy_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_proxy_testing) | [maps_core_mobile_http2_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_http2_testing) |
| Stress | [maps_core_mobile_proxy_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_proxy_stress) | [maps_core_mobile_http2_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_mobile_http2_stress) |

## Graphics dashboards
| Staging | SPDYS | HTTP/2 |
|---|---|---|
| **Main panel** | | |
| Stable+Prestable | [maps_core_mobile_proxy](https://yasm.yandex-team.ru/panel/maps_core_mobile_proxy/) | [maps_core_mobile_http2](https://yasm.yandex-team.ru/panel/maps_core_mobile_http2/) |
| Prestable | [maps_core_mobile_proxy](https://yasm.yandex-team.ru/panel/maps_core_mobile_proxy_prestable) | [maps_core_mobile_http2](https://yasm.yandex-team.ru/panel/maps_core_mobile_http2_prestable) |
| Testing | [maps_core_mobile_proxy_testing](https://yasm.yandex-team.ru/panel/maps_core_mobile_proxy_testing/) | [maps_core_mobile_http2_testing](https://yasm.yandex-team.ru/panel/maps_core_mobile_http2_testing/) |
| Stress | [maps_core_mobile_proxy_stress](https://yasm.yandex-team.ru/panel/maps_core_mobile_proxy_stress/) | [maps_core_mobile_http2_stress](https://yasm.yandex-team.ru/panel/maps_core_mobile_http2_stress/) |
| **SEDEM-generated**  | | |
| Stable+Prestable | [maps-core-mobile-proxy-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-proxy-stable-panel-main) | [maps-core-mobile-http2-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-http2-stable-panel-main) |
| Prestable | [maps-core-mobile-proxy-prestable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-proxy-prestable-panel-main) |  [maps-core-mobile-http2-prestable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-http2-prestable-panel-main) |
| Testing | [maps-core-mobile-proxy-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-proxy-testing-panel-main) |  [maps-core-mobile-http2-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-http2-testing-panel-main) |
| Stress | [maps-core-mobile-proxy-stress-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-proxy-stress-panel-main) |  [maps-core-mobile-http2-stress-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-mobile-http2-stress-panel-main) |

## Client access and ratelimiting
Clients are distinguished by their key(client_id). There are 2 sources of knowledge about keys:
* [apikeys](https://admin-developer.tech.yandex-team.ru/)
* [ratelimiter config in Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_mobile/)

After commit to ratelimiter config or every 15 minute [MAPS_MOBILE_ACCESS_UPDATER](https://sandbox.yandex-team.ru/scheduler/16338/view) Sandbox task is launched. It first fetches data from apikeys, merges it with ratelimiter config (can be used to override) to one single JSON and uploads it to [Ecstatic](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-mobile-access-config/versions).

Every key belongs to one of three categories: free, commercial, yandex.

Handles in mobile proxy are also marked as yandex_only, offline_caches, freemium or none

Ratelimiter is checking against two quotas
* **<(key or default), handle@client_type>**
* **<(key or default), handle_type@client_type>**

There may be personal quota in ratelimiter config for some key, otherwise default one is used.

For example **<default, yandex_only@free>** and **<default, yandex_only@commercial>** quota are 0, which means that not yandex apps cannot access yandex_only handles.

There also may be extra restrictions, that key can be used only with specific app_id.

If quota is exceeded 429 code is answered and request is not passed to the backend. A specific case is when quota is 0, then 403 is returned.

403 is also returned in following cases:
* It came from upstream (from_upstream)
* Bad signature (bad_signature)
* Key is unknown (not_whitelisted)
* Key is banned (blacklisted)
* Endpoint was not found (unknown_endpoint_group)

For each case there is specific monitoring.

### Blocking certain applications
* You CAN block certain applications by editing [Black list configs](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_mobile/black_list).
  Your black list entry MUST have an `app_id`. You MAY also specify `key` and/or `version` filter.
* Alternatively you can unblock certain app [White list configs](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_mobile/white_list)

### Ssl-ratelimiter
There is also ssl-handshake ratelimiter on http2 proxy with current limit of 300 hps for one instance.
[Ssl-handshake Graphics](https://yasm.yandex-team.ru/chart/signals=aux-handshakes_*;hosts=ASEARCH;itype=maps;ctype=prestable,stable;prj=maps-core-mobile-http2/)

### Stat reports for API Keys
|---|
| [Daily shared quota](https://stat.yandex-team.ru/Maps_Plus_Beta/MapKit/Apps/clients_freemium) |
| [Daily total requests](https://stat.yandex-team.ru/Maps_Plus_Beta/MapKit/Apps/clients_hits) |
| [RPS](https://stat.yandex-team.ru/Maps_Plus_Beta/MapKit/Apps/clients_rps) |

### Ratelimiter panel
[RPS and Quotas](https://yasm.yandex-team.ru/template/panel/maps_mobile-ratelimiter2-panel)

## Monitorings
| Type | SPDYS | HTTP/2 |
|---|---|---|
| Juggler (All) | https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-mobile-proxy | https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-mobile-http2 |
| Juggler (Stable) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_proxy_stable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_http2_stable |
| Juggler (Prestable) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_proxy_prestable | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_http2_prestable |
| Juggler (Testing) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_proxy_testing | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_http2_testing |
| Juggler (Stress) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_proxy_stress | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_mobile_http2_stress |

## SLA
[maps_mobile.py](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_mobile.py).

## What happens when service is down
Clients are not able to get maps, nor build routes, nor use geo search, nor use any of maps mobile APIs.

## How to fix common problems
* [The table of the responsible](https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/maps_mobile/) contains [the checklist of things to do when our handmade monitorings fire](https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/maps_mobile/#checklist).
* How to find out on which host happens something strange? You may "split by hosts" signal in Golovan. But keep in mind that many monitorings are designed to be 0 if signal is less than some threshold (e.x. rps < 10). In such case first remove this truncation, otherwise in split by host mode signal may be 0 for every host. Another moment is that there are more than thousand hosts in group, so it is more useful to use "top by hosts" mode. Same note about threshold applies here and be quick this mode works only for last 25 minutes in Golovan. [Another way to split signal by hosts](https://yasm.yandex-team.ru/template/panel/maps_core_mobile_by_host/signal=roquefort-external_ok_ammv/). executer application may also be usefull to grep logs on multiple hosts.
* In case of 429:
  * Check in logs if 429 are from upstream, if yes contact upstream responsible
  * If it is because of ratelimiter quoatas are exceeded, than find out from logs: app_id (user_agent), key (mapkit_client_id) and client type. To determine client type you may run `cat /var/lib/yandex/maps/ecstatic/data/yandex-maps-mobile-access-config/access-config.json | grep -n5 $key`. In case of commercial client contact B2B team (see bellow). Maybe there is need to temporaly override limit or client type in case of big commercial client.
    In case of Yandex app inform its developers and be ready to increase limit in ratelimiter config in Arcadia.
* In case of 403 monitorings:
  * bad_signature - there is always litle rate of requests from scripts. In case of big splash, check whether it is a some kind of attack or problem with our signature checker?
  * unknown_endpoint_group - should never be fired, probably means there is a bug in our ratelimiter lua-script.
  * from_upstream - contact upstream responsible.
  * blacklisted - splashes may be if B2B banned some client or it was added to blacllist in arcadia. Contact B2B team (see bellow) to ensure there was no mistake.
  * not_whitelisted - splashes may be:
    * if B2B removed or manually banned some client or it was removed from whitelist in arcadia. Contact B2B team (see bellow) to ensure there was no mistake.
    * it may be automatic ban from apikeys if client exceeded it dayly quota from apikeys point of view. In this case it is also reasonable to inform B2B.
    * Should not happen with Yandex app, in such case check whether MAPS_MOBILE_ACCESS_UPDATER task is working correctly.

  **B2B team contacts: Anton Tokbulatov (atokbulatov@yandex-team.ru) or Ekaterina Chernysheva (ryabchikova@yandex-team.ru).**

* [Ratelimiter alerts troubleshooting](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ratelimiter2/agent_troubleshooting.md)
* [auth_agent alerts troubleshooting](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/auth_agent/troubleshooting.md)
* [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
* To detach whole DC use ITS. Press "Apply" button on the maps-core-mobile-{http2|proxy}-{stable|prestable}:
  * SAS: https://nanny.yandex-team.ru/ui/#/its/locations/maps/sas/backend_detach/
  * VLA: https://nanny.yandex-team.ru/ui/#/its/locations/maps/vla/backend_detach/
  * MAN: https://nanny.yandex-team.ru/ui/#/its/locations/maps/man/backend_detach/

  To attach back use "trash bin" button.
* If fixing a problem requires restarting nginx, at least pre-check config validity:

  `nginx -t && supervisorctl restart nginx`

  If restart is not urgent, please also refrain hitting users with broken connections by temporary firewalling and delaying restart:

  ```
  iptruler all down
  sleep 5
  nginx -t && supervisorctl restart nginx
  iptruler all up
  ```
* To disable SSL-handshake limits run the following script:

  `/usr/lib/yandex/maps/handshake-counters/disable.sh`

  To enable it again:

  `/usr/lib/yandex/maps/handshake-counters/enable.sh`

## Logs

### Locations on instances
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |

### YQL
access-log is available via YQL.

The new table, containg exclusively Maps Core Mobile Proxy (both SPDY and HTTP/2) logs, is logs/maps-core-mobile-access-log in the Hahn cluster.

Access to logs/maps-core-mobile-access-log is restricted. You may [request access on IDM](https://idm.yandex-team.ru/#rf-role=AWf83PnN#yt-hahn/maps-core-mobile-access-log-ro;;;,rf-expanded=AWf83PnN,rf=1).

[logs/maps-core-mobile-access-log YQL to 1d logs example](https://yql.yandex-team.ru/Operations/X7PMyRpqvyNgOb2h1ipWoDqPMdDjNgxVHmQiHBlABoQ=).
[logs/maps-core-mobile-access-log YQL to 5min log stream](https://yql.yandex-team.ru/Operations/X7PM5BpqvyNgOb27OQFe2noyAFBGl4H-nemQc9sGL4o=).

## Balancers
| Staging | SPDY URL | HTTP/2 URL
|---|---|---|
| Stable+Prestable | spdy3.mob.maps.yandex.net: [L3 manager](https://l3.tt.yandex-team.ru/service/2413), [AWACS](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-mobile-proxy.maps.yandex.net/show/) | proxy.mob.maps.yandex.net: [L3 manager](https://l3.tt.yandex-team.ru/service/7158), [AWACS](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-mobile-http2.maps.yandex.net/show/)
| MAN only Stable+Prestable | | man.proxy.mob.maps.yandex.net: [L3 manager](https://l3.tt.yandex-team.ru/service/12713), [AWACS](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/man.core-mobile-http2.maps.yandex.net/show/)
| Testing | spdy3.mob.tst.maps.yandex.net: [L3 manager](https://l3.tt.yandex-team.ru/service/5187), [AWACS](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-mobile-proxy.testing.maps.yandex.net/show/) | proxy.mob.tst.maps.yandex.net: [L3 manager](https://l3.tt.yandex-team.ru/service/7258), [AWACS](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-mobile-http2.testing.maps.yandex.net/show/)

## Known clients
* Mobile Yandex.Maps, Navi, Taxi, Drive, Auto, Search App, Browser, Transport, Toloka
* [Public MapKit](https://tech.yandex.com/maps/mapkit/) users: Sberbank, Cian, and many more

## Ecstatic Datasets
Stable, prestable:
* yandex-maps-mobile-access-config

Testing, stress:
* yandex-maps-test-mobile-access-config

## Sandbox Resources
[A small text file](https://sandbox.yandex-team.ru/resource/910299721/view) is used in a [maps/mobile/server/tools/signature](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/tools/signature) test.

## Persistent Volumes
/persistent - a partition for persistent data storage (i.e. for data that needs to survive redeployments). Symlinks:
* /var/lib/yandex/maps/ecstatic - all ecstatic data
* /etc/yandex/maps/rate-limiter/config - rate-limiter config delivered by ecstatic

/logs - a persistent partition for logs. Symlink: /var/log

## Firewall macros
| staging | URL | HTTP/2 URL
|---|---|---|
| Stable, Prestable | [ \_MAPS_CORE_MOBILE_PROXY_STABLE_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MOBILE_PROXY_STABLE_RTC_NETS_ ) | [ \_MAPS_CORE_MOBILE_HTTP2_STABLE_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MOBILE_HTTP2_STABLE_RTC_NETS_ ) |
| Testing, Stress | [ \_MAPS_CORE_MOBILE_PROXY_TESTING_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MOBILE_PROXY_TESTING_RTC_NETS_ ) | [ \_MAPS_CORE_MOBILE_HTTP2_TESTING_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MOBILE_HTTP2_TESTING_RTC_NETS_ ) |

## Stress testing
Production traffic experiments have shown that proxy CPU can handle 2100 rps/core (25 000 rps/instance) of SPDY traffic. CPU is the bottleneck for SPDY traffic. This result was verified with ad hoc shootings using yandex-mapsmobi-tools-downloader.

Lunapark shootings have shown that proxy CPU can handle 5000-5500 rps/core of either HTTP/2 or HTTPS traffic. In this case, TLS handshakes consume significant amount of CPU.

[More information about shootings](https://wiki.yandex-team.ru/users/iudalov/maps-mobile-RTC/)

After migrating to HTTP/2 protocol regression shootings were implemented. They use [a scheduler](https://sandbox.yandex-team.ru/scheduler/23357) which launches at 02:00 every day. It uses configs and ammo [from Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/proxy/regression). It is not in an ideal state; some current problems are described [here](https://wiki.yandex-team.ru/users/selivni/o-reguljarnyx-regressionnyx-strelbax-po-prokse/#izvestnyeproblemy) (can become obsolete soon).

## Quorum
For safety reasons, a certain "quorum" mechanic is used in mobile proxy: if amount of "healthy" pods in one datacenter gets lower than 60% of total number of pods, the l3 balancer cuts the whole datacenter off from traffic. It is done to prevent datacenter overload. To get the balancer to accept this datacenter back, you need to make at least 70% of pods respond to its pings.
If, however, you need to disable quorum for a while (for instance, to stress-test the proxy) and you have appropriate rights to access the l3 balancer, you can do so in few simple steps:
1. Go to [L3 manager page for http/2 proxy](https://l3.tt.yandex-team.ru/service/7158), click on an active configuration and press `Edit`
2. For each server in `Virtual servers` list:
1. Press `Edit`
2. In `Advanced settings` put some small non-null value (e. g. `10%`) into `QUORUM` field, and `0%` into `HYSTERESIS` field
3. Scroll waaay down the long list of RS's and press `Save changes`
3. Make sure everything is correct, then press `Save` button
4. Wait until the new configuration deploys completely. It may fail to get commited, or fail some tests. In most cases, if you're sure your config is correct, simply restarting the deploy sequence will work
5. After you're done, don't forget to return everything to its place. Do everything listed above once again, with `QUORUM = 65%` and `HYSTERESIS = 5%`
