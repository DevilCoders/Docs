# Maps Automotive Proxy

Entry point for automotive services

| What | Who |
| ---- | --- |
| Responsible SE | Mikhail Kupriyanov (kupriyanov-m@yandex-team.ru) |
| Responsible SRE | Mikhail Krutyakov (mkrutyakov@yandex-team.ru) |
| Source code | https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/proxy |
| ABC-service | https://abc.yandex-team.ru/services/maps-auto-proxy/ |
| CI (TestEnv) | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_PROXY |
| Wiki | https://wiki.yandex-team.ru/Automotive/serverdevelopment/maps-auto-proxy/ |

## Documentation
This proxy is based on [yacare base image](https://wiki.yandex-team.ru/maps/dev/core/yacare/).

## What happens when the service is down
The service is entry point for the automotive services. When it's down, software updates, radio stations list, autoparking feature and automotive store become unavailable.

Services listed in [upstreams configuration](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/proxy/config/upstreams/yandex-auto-proxy.upstreams.production) will be unavailable for automotive head units. Here is a list of those services (make sure that README is up-to-date and matches the upstreams config):

- [Parking API](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/fastcgi/parking_api#what-happens-when-service-is-down)
- [Parking Receiver](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/fastcgi/parking_receiver#what-happens-when-service-is-down)
- [Updater](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/updater#what-happens-when-service-is-down)
- [Jams Matcher](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/modules/matcher#what-happens-when-service-is-down)
- [Startrek Proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/startrek-proxy#what-happens-when-service-is-down) — bug-reports from head units won't be saved in Startrek and YT

## Troubleshooting

- **maps_auto_proxy_stable:total-404** Those may be requests from a **crasher** (security service utility). See logs to check if there are query parameters `everybodybecoolthisis=crasher` or `everybodybecoolthisis=molly` in requests. (NB: some acknowledged experts can see it from the specific shape of "Total RPS codes" graphic.)
- **maps_auto_proxy_stable:default_tcp_check** Usually that happens because of drills or someone messing with service settings. Ask about it in chat. If not, situation requires further investigation.
- **maps_auto_proxy_stable:ratelimiter** Someone must be trying to send too many reports. Maybe those people are testers. Usually that's not a problem, but we need to understand why that happened. If such problems start to occur too often, we should consider increasing our ratelimiter limits or doing some other appropriate thing.

Following are some curl requests to check whether proxy works (some may respond with codes other than 200, but that's OK):

```
OAUTH=<your_oauth_token>

curl -X GET https://automotive.yandex.net/ping

# /reports

curl -X POST https://automotive.yandex.net/reports/1.x/upload_file?device_id=0123456789abcdef0123456789abcdef \
    -H 'Content-Type: apllication/zip' \
    -H 'X-YRuntime-Timestamp: 1594397797' \
    -H 'X-YRuntime-Signature: A2gb2Q+dFqTxjHGl/zRHq8t+AtU=' \
    -d 'Dummy report data'

curl -X POST https://automotive.yandex.net/reports/1.x/upload_report?head_id=012345abcdef\&device_id=0123456789abcdef0123456789abcdef \
    -H 'Content-Type: apllication/zip' \
    -H "Authorization: OAuth $OAUTH" \
    -H 'X-YRuntime-Timestamp: 1594397797' \
    -H 'X-YRuntime-Signature: A2gb2Q+dFqTxjHGl/zRHq8t+AtU=' \
    -d 'Dummy report data'

# /parking

curl -X POST https://automotive.yandex.net/parking/1.x/stop_session?session_id=0123456789abcdef0123456789abcdef \
    -H "Authorization: OAuth $OAUTH"

curl -X GET https://automotive.yandex.net/parking/1.x/active_sessions?device_id=0123456789abcdef0123456789abcdef \
    -H "Authorization: OAuth $OAUTH"

curl -X POST https://automotive.yandex.net/parking/1.x/register_device?device_id=0123456789abcdef0123456789abcdef \
    -H "Authorization: OAuth $OAUTH"

# /radio

curl -X GET https://automotive.yandex.net/radio/1.x/stationlist?lang=ru_RU \
    --output -

# /updates

curl -X POST https://automotive.yandex.net/updater/1.x/updates?vendor=toyota\&model=rav4\&mcu=caska\&lang=ru_RU\&uuid=\&headid=abcdef012345 \
    -d '[{"package": "ru.yandex.yandexnavi", "version": { "code": 1, "text": "1.0"}}, { "package": "yandex.auto", "version": { "code" : 0, "text": "0.0"}}]'

curl -X POST https://automotive.yandex.net/updater/1.x/firmware_updates?vendor=toyota\&model=rav4\&mcu=caska\&lang=ru_RU\&uuid=\&headid=abcdef012345 \
    -d '{"ro.build.date.utc": 1594397797}'
    
curl -X POST https://automotive.yandex.net/updater/2.x/updates?vendor=toyota\&model=rav4\&mcu=caska\&lang=ru_RU\&uuid=\&headid=abcdef012345

# /datacollect

curl -X POST https://automotive.yandex.net/datacollect/1.x/gps_signals \
    -H "Authorization: OAuth $OAUTH"

curl -X POST https://automotive.yandex.net/datacollect/1.x/vehicle_data?device_id=0123456789abcdef0123456789abcdef \
    -H "Authorization: OAuth $OAUTH"
```

## Deploy
Important: deploy your builds only on Mondays—Thursdays, between 12:00 and 20:00 Moscow Time.
1. After a commit to maps/automotive/proxy, TestEnv will trigger build automatically, new Docker image will be pushed to the maps/auto-proxy repository, you will receive e-mail with build task status.
2. Use SEDEM to deploy your version: sedem release step . $your_version testing/prestable/stable
3. Check monitorings and graphics after your release to be sure everything went OK


## Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| **Common** | [Nanny Panel](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_auto_proxy/) | - | [Juggler Dashboard](https://juggler.yandex-team.ru/dashboards/maps_auto_proxy/) |
| Testing | [maps_auto_proxy_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_proxy_testing/) | [ auto-proxy.testing ](https://yasm.yandex-team.ru/template/panel/maps-auto-proxy-testing-panel-main/) | [ maps_auto_proxy_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_proxy_testing) |
| Prestable | [maps_auto_proxy_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_proxy_prestable/) | [ auto-proxy.prestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-proxy-prestable-panel-main/) | [ maps_auto_proxy_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_proxy_prestable) |
| Stable | [maps_auto_proxy_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_proxy_stable/) | [ auto-proxy.stable ](https://yasm.yandex-team.ru/template/panel/maps-auto-proxy-stable-panel-main/) | [ maps_auto_proxy_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_proxy_stable) |
| Stress | [maps_auto_proxy_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_proxy_stress/) | [ auto-proxy.stress ](https://yasm.yandex-team.ru/template/panel/maps-auto-proxy-stress-panel-main/) | [ maps_auto_proxy_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_proxy_stress) |
[Monitorings all (tag=a_prj_maps-auto-proxy)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-auto-proxy)

**Ratelimiter panel:** [RPS and Quotas](https://yasm.yandex-team.ru/template/panel/maps_auto_proxy-ratelimiter2-panel/)

## YP pods
| Staging | YP Pod |
| ------- | ------ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_proxy_testing/yp_pods/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_proxy_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_proxy_stable/yp_pods/ |
| Stress | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_proxy_stress/yp_pods/ |


## Firewall macroses
| Staging | URL |
|---|---|
| Stable | [ \_MAPS_AUTO_PROXY_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_PROXY_STABLE_RTC_NETS_ ) |
| Testing | [ \_MAPS_AUTO_PROXY_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_PROXY_TESTING_RTC_NETS_ ) |


## Balancers
| Staging | URL |
| ------- | --- |
| Testing | auto-proxy.testing.maps.yandex.net [L3 Manager](https://l3.tt.yandex-team.ru/service/7518), [AWACS](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-proxy.testing.maps.yandex.net/show/) |
| Stable + Prestable | auto-proxy.maps.yandex.net [L3 Manager](https://l3.tt.yandex-team.ru/service/7527), [AWACS](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-proxy.maps.yandex.net/show/) |


## BlackBox grants

Search for maps-auto-proxy in this [form](https://grantushka.yandex-team.ru/grants/consumer/).
Generaly this proxy uses BlackBox grants to exchange incoming OAuth for user ticket and use that ticket for authorization in proxied services.

## Logs
| Name                      | URL/path |
|---------------------------|----------|
| Nginx                     | /var/log/nginx/* |
| Yacare auth-agent         | /var/log/yandex/maps/auth_agent/* |
| Yacare ratelimiter2-proxy | /var/log/yandex/maps/ratelimiter-proxy/* |
| Supervisord               | /var/log/supervisor/* |
| Syslog (unified)          | /var/log/syslog |
| YT                        | https://yql.yandex-team.ru : ``SELECT * FROM hahn.`logs/maps-log/1d/2020-06-20` WHERE (vhost LIKE 'automotive.yandex.net' OR vhost LIKE 'auto-proxy.maps.yandex.net') AND service_name LIKE 'auto-proxy' limit 1;`` |


## How to fix common problems

* [Ratelimiter alerts troubleshooting](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ratelimiter2/agent_troubleshooting.md)
* [auth_agent alerts troubleshooting](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/auth_agent/troubleshooting.md)
* [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
* **Certificate expires.** Manually order a new certificate using [CRT Service](https://crt.yandex-team.ru/certificates), replace it in nanny service's "Instance Spec" in both prestable and stable environments ("Instance data volumes", "properties.d" volume, change YA Vault secret). After deployment you can examine certificate properties using openssl, e.g.:
```bash
echo | openssl s_client -showcerts -servername automotive.yandex.net -connect maps-auto-proxy-prestable-2.sas.yp-c.yandex.net:443 2>/dev/null | openssl x509 -inform pem -noout -text
```

## Known clients

* Head-Units Software ([Launcher](https://wiki.yandex-team.ru/Automotive/description/), Remote Task Manager, etc.)


## Regression Stress Testing Configurations

| Type | URL |
|---|---|
| Sandbox scheduler for regular stress testing with constant rps | https://sandbox.yandex-team.ru/scheduler/22613 |
| Sandbox scheduler for regular stress testing with linear rps | https://sandbox.yandex-team.ru/scheduler/22614 |
| Tracker ticket for constant rps | https://lunapark.yandex-team.ru/YCARBACKEND-476 |
| Tracker ticket for linear rps | https://lunapark.yandex-team.ru/YCARBACKEND-477 |
| CI | https://lunapark.yandex-team.ru/regress/YCARBACKEND |


## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_auto_proxy)
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_auto_proxy.py)


## SECAUDIT

https://st.yandex-team.ru/SECAUDIT-3280


## How to run it locally

If you need to run proxy's Docker-container locally, use the following command:

```
sudo docker run -it --net host \
    auto-proxy:1.0 bash
```

Inside of the container run:

```
rm /etc/runner/run.d/19_concat_key_with_cert.sh
rm /etc/nginx/conf.d/01-ssl.conf

/etc/runner/run.sh
```

You may also need to set some variables, e.g. `AUTOMOTIVE_HTTP_SIGNATURE_KEY` or `REPORTS_ROBOT_STARTREK_OAUTH_TOKEN` in order to make specific endpoints work properly. You may use current testing or stress Nanny configuration as a reference.

## Quorum
A certain "quorum" mechanic is used in auto proxy: if amount of "healthy" pods in one datacenter gets lower than 2, the l3 balancer cuts the whole datacenter off from traffic. It is done to prevent datacenter overload. To get the balancer to accept this datacenter back, you need to make at least 2 pods respond to its pings.
If, however, you need to disable quorum for a while and you have appropriate rights to access the l3 balancer, you can do so in few simple steps:
1. Go to [L3 manager page for auto proxy](https://l3.tt.yandex-team.ru/service/7527), click on an active configuration and press `Edit`
2. For each server in `Virtual servers` list:
  1. Press `Edit`
  2. In `Advanced settings` put `1` into `QUORUM` field
  3. Scroll waaay down the long list of RS's and press `Save changes`
3. Make sure everything is correct, then press `Save` button
4. Wait until the new configuration deploys completely. It may fail to get commited, or fail some tests. In most cases, if you're sure your config is correct, simply restarting the deploy sequence will work
5. After you're done, don't forget to return everything to its place. Do everything listed above once again, with `QUORUM = 2`

