# Yandex.Courier.Backend

Yandex.Routing: Delivery Monitoring Backend.

[[toc]]

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | [abc:maps-b2bgeo-courier](https://abc.yandex-team.ru/services/maps-b2bgeo-courier/) |
| Отвественные SRE | Elena Markova (4c4d@yandex-team.ru) |
| Исходники | [maps/b2bgeo/ya_courier/backend](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/ya_courier/backend) |
| Сервис в ABC | [maps-b2bgeo-courier](https://abc.yandex-team.ru/services/maps-b2bgeo-courier/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_B2BGEO_COURIER |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_b2bgeo_courier_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_courier_prestable/) | [ b2bgeo-courier.prestable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-courier-prestable-panel-main/) | [ maps_b2bgeo_courier_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_courier_prestable) |
| Stable | [maps_b2bgeo_courier_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_courier_stable/) | [ b2bgeo-courier.stable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-courier-stable-panel-main/) | [ maps_b2bgeo_courier_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_courier_stable) |
| Stress | [maps_b2bgeo_courier_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_courier_stress/) | [ b2bgeo-courier.stress ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-courier-stress-panel-main/) | [ maps_b2bgeo_courier_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_courier_stress) |
| Testing | [maps_b2bgeo_courier_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_courier_testing/) | [ b2bgeo-courier.testing ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-courier-testing-panel-main/) | [ maps_b2bgeo_courier_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_courier_testing) |

[Monitorings all (tag=a_prj_maps-b2bgeo-courier)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-b2bgeo-courier)

[Custom dashboard](https://yasm.yandex-team.ru/template/panel/b2bgeo_yacourier_backend-template/env=-prod/)

[Corpse dashboard](https://corpse.yandex-team.ru/b2bgeo_delivery)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [b2bgeo-courier.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/b2bgeo-courier.maps.yandex.net/) | [b2bgeo-courier.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=b2bgeo-courier.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,man,sas;prj=b2bgeo-courier-maps;signal=service_total) | [rtc_balancer_b2bgeo-courier_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-courier_maps_yandex_net_man)<br>[rtc_balancer_b2bgeo-courier_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-courier_maps_yandex_net_sas)<br>[rtc_balancer_b2bgeo-courier_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-courier_maps_yandex_net_vla) |
| Testing | Default | [b2bgeo-courier.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/b2bgeo-courier.testing.maps.yandex.net/) | [b2bgeo-courier.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=b2bgeo-courier.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=vla,sas;prj=b2bgeo-courier-testing-maps;signal=service_total) | [rtc_balancer_b2bgeo-courier_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-courier_testing_maps_yandex_net_sas)<br>[rtc_balancer_b2bgeo-courier_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_b2bgeo-courier_testing_maps_yandex_net_vla) |


## Documentation
- [Official documentation](https://yandex.ru/routing/doc/delivery/)
- [OpenAPI spec](https://courier.yandex.ru/api/v1/doc)


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_B2BGEO_COURIER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_COURIER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_B2BGEO_COURIER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_COURIER_TESTING_RTC_NETS_ ) |


## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/* |
| Access log (YT) | https://yql.yandex-team.ru : ```SELECT * FROM hahn.`logs/maps-log/1d/2021-11-10` WHERE vhost LIKE 'courier.yandex.%' limit 1;``` |
| YCB service (YT; testing) | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/b2bgeo-courier-testing |
| YCB service (YT; stable) | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/b2bgeo-courier-stable |


## Databases
| Staging | YC | Ya Vault secret |
|---|---|---|
| Stress | https://yc.yandex-team.ru/folders/fooooj7at8f8673omia9/managed-postgresql/cluster/mdb4897aq0mdvv74pgp7 | https://yav.yandex-team.ru/secret/sec-01f4ccrsqh07t6fz715yhsv9fp/explore/versions |
| Testing | https://yc.yandex-team.ru/folders/fooooj7at8f8673omia9/managed-postgresql/cluster/31e78a61-60b0-405e-a531-810a82f00ff7 | https://yav.yandex-team.ru/secret/sec-01ddnqwesjbm5yjadwh1fpky75/explore/versions |
| Production | https://yc.yandex-team.ru/folders/fooooj7at8f8673omia9/managed-postgresql/cluster/85a09555-ae39-4852-91b0-41d64fcf56bf | https://yav.yandex-team.ru/secret/sec-01ddr3wjvshqapcjd6fj8czpp2/explore/versions |


## Domains
| Staging | Domains |
|---|---|
| Testing | test.api.courier.yandex.net, test.courier.yandex.com, test.courier.yandex.com.tr, test.courier.yandex.ru, test.mobile.courier.yandex.net |
| Production | api.courier.yandex.net, courier.yandex.com, courier.yandex.com.tr, courier.yandex.ru, mobile.courier.yandex.net |


## Acceptance tests

[YA_COURIER_BACKEND_INTEGRATION_TESTS](https://sandbox.yandex-team.ru/tasks?children=false&hidden=true&type=BBGEO_YA_COURIER_INTEGRATION_TESTS&limit=20&created=14_days)


## Ratelimiter
We use ratelimiter for limiting `/couriers/<courier_id>/routes/<route_id>/push-positions-v3` rps.

Ratelimiter config: https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_b2bgeo_ya_courier/stable.yaml

Ratelimiter panel: https://yasm.yandex-team.ru/template/panel/maps_b2bgeo_ya_courier-ratelimiter2-panel/


## How to update service manually
In emergency cases when sandbox is too slow to be used we agreed to update service manually.
Steps:
1. You'll need docker to be installed
  - [Docker for Mac](https://docs.docker.com/docker-for-mac/)
2. Receive [Yandex registry token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1)
3. Login to the registry:
```sh
docker login -u ${yandex_login} -p ${registry_token} registry.yandex.net
```
4. Update your arcadia folder and revert any irrelevant changes you've made
5. Build & upload docker image, here $REVISION is your svn revision number:
```sh
cd ~/arcadia/maps/b2bgeo/ya_courier/backend
ya package --custom-version=$REVISION docker/pkg.json
docker build -t registry.yandex.net/b2bgeo/ya-courier-backend:$REVISION-local  - < maps-b2bgeo-ya-courier-backend.$REVISION.tar.gz
docker push registry.yandex.net/b2bgeo/ya-courier-backend:$REVISION-local
```
6. Update ya-courier-backend testing
7. Update ya-courier-backend production


## Troubleshooting
https://wiki.yandex-team.ru/b2bgeo/dev/helpdesk/troubleshooting/


## Usage
- Register your application using [Yandex.Oauth](https://oauth.yandex.ru/client/new) to get application ID.
Yandex.Courier -> Logistician Role should be checked.

- Login to Yandex.Passport with registered Yandex account and receive your token via link https://oauth.yandex.ru/authorize?response_type=token&client_id=YOUR_APPLICATION_ID_HERE.
Also you can use test application [token](https://oauth.yandex.ru/authorize?response_type=token&client_id=a7c29e6d02b34727902f172308e618eb). This way is recommended for test purposes only.


## Release process
Deploy process is described on [wiki page](https://wiki.yandex-team.ru/b2bgeo/dev/yacourier/#howtodeployservice).


## Signature check

Signature verification is implemented for `/couriers/<courier_id>/routes/<route_id>/push-positions-v3` handler.

To add new signature secret:
1. Add alias for apikey to [map in lua script](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/ya_courier/backend/docker/install/usr/lib/yandex/maps/yacare/lua/init.d/03-init-http-signature.lua?rev=7471599#L10)
2. Add rps limit for the alias to [ratelimiter config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_b2bgeo_ya_courier/stable.yaml?rev=7471169#L8)
3. Generate random hexadecimal number of length 32:
```sh
tr -dc a-f0-9 < /dev/urandom | head -c 32; echo ''
```
4. Update secret in [Vault service](https://yav.yandex-team.ru/secret/sec-01ememje8x59sg7rzmb33kps1d/explore/versions).
5. Update secret version in [sedem config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/ya_courier/backend/sedem_config/secrets.yaml?rev=r8646092#L77)
6. Deploy YCB.
