# Auto Radio

Provides information about radiostations and radiotowers for automotive head units and Alice (megamind).

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Михаил Крутяков (mkrutyakov@yandex-team.ru) |
| Отвественные SRE | Михаил Куприянов (kupriyanov-m@yandex-team.ru)<br>Михаил Крутяков (mkrutyakov@yandex-team.ru) |
| Исходники | [maps/automotive/radio_service](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/radio_service) |
| Сервис в ABC | [maps-auto-radio](https://abc.yandex-team.ru/services/maps-auto-radio/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_RADIO |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_auto_radio_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_radio_prestable/) | [ auto-radio.prestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-radio-prestable-panel-main/) | [ maps_auto_radio_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_radio_prestable) |
| Stable | [maps_auto_radio_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_radio_stable/) | [ auto-radio.stable ](https://yasm.yandex-team.ru/template/panel/maps-auto-radio-stable-panel-main/) | [ maps_auto_radio_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_radio_stable) |
| Testing | [maps_auto_radio_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_radio_testing/) | [ auto-radio.testing ](https://yasm.yandex-team.ru/template/panel/maps-auto-radio-testing-panel-main/) | [ maps_auto_radio_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_radio_testing) |


[Monitorings all (tag=a_prj_maps-auto-radio)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-auto-radio)

**Testing** is also used as stress for regression tests.

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [auto-radio.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-radio.maps.yandex.net/) | [auto-radio.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=auto-radio.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=auto-radio-maps;signal=service_total) | [rtc_balancer_auto-radio_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-radio_maps_yandex_net_man)<br>[rtc_balancer_auto-radio_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-radio_maps_yandex_net_sas)<br>[rtc_balancer_auto-radio_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-radio_maps_yandex_net_vla) |
| Testing | Default | [auto-radio.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-radio.testing.maps.yandex.net/) | [auto-radio.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=auto-radio.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,man;prj=auto-radio-testing-maps;signal=service_total) | [rtc_balancer_auto-radio_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-radio_testing_maps_yandex_net_man)<br>[rtc_balancer_auto-radio_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-radio_testing_maps_yandex_net_sas) |

### Ecstatic datasets

**yandex-maps-fm-radio:**
- [stable](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ecstatic/stable/yandex-maps-fm-radio.conf)
- [testing](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ecstatic/testing/yandex-maps-fm-radio.conf)

## What happens when service is down

Head units won't receive new information about radio towers and default stations. Also requests to Alice about radio (on head units) will fail (e.g. "turn on radio Maximum").

Sample queries to check if radio service works:

(testing)
```bash
curl http://maps-auto-radio-testing-1.man.yp-c.yandex.net/radio/1.x/stationlist \
    -H 'Host: auto-radio.testing.maps.yandex.net'

curl -X POST http://maps-auto-radio-testing-1.man.yp-c.yandex.net/radio/1.x/mm/run \
    -H 'Host: auto-radio.testing.maps.yandex.net' \
    -d 'BaseRequest {
  ClientInfo {
    AppId: "yandex.auto"
    AppVersion: "1.4.5"
    Lang: "ru_RU"
  }
  Location {
    Lat: 55.753215
    Lon: 37.622504
  }
}
Input {
  SemanticFrames {
    Name: "alice.automotive.fm_radio_play"
    Slots {
      Name: "fm_radio"
      Value: "маяк"
    }
  }
  Text {
    RawUtterance: "включи радио маяк"
    Utterance: "включи радио маяк"
  }
}'
```

To check stable use hostname auto-radio.maps.yandex.net

You also should check whether Alice works correctly with a service. In order to do so in testing you may use Telegram bot @AmandaJohnsonBot. Set megamind host to DEV: http://megamind-ci.alice.yandex.net/speechkit/app/pa/ And set AppId to yandex.auto After that you may ask bot to enable specific radio and see whether there is an answer like the following or not:

```
yandexauto://fm_radio?frequency=10370&name=%D0%A0%D0%B0%D0%B4%D0%B8%D0%BE%20%D0%9C%D0%B0%D0%BA%D1%81%D0%B8%D0%BC%D1%83%D0%BC
```

## Alice configuration files

| Staging | Alice staging | File location |
| ------- | ------------- | ------------- |
| Testing | Dev           | [AutomotiveRadio.pb.txt](https://a.yandex-team.ru/arc/trunk/arcadia/alice/megamind/configs/dev/scenarios/AutomotiveRadio.pb.txt) |
| Stable  | Hamster       | [AutomotiveRadio.pb.txt](https://a.yandex-team.ru/arc/trunk/arcadia/alice/megamind/configs/hamster/scenarios/AutomotiveRadio.pb.txt) |
| Stable  | RC            | [AutomotiveRadio.pb.txt](https://a.yandex-team.ru/arc/trunk/arcadia/alice/megamind/configs/rc/scenarios/AutomotiveRadio.pb.txt) |
| Stable  | Production    | [AutomotiveRadio.pb.txt](https://a.yandex-team.ru/arc/trunk/arcadia/alice/megamind/configs/production/scenarios/AutomotiveRadio.pb.txt) |

## Logs

| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/auto-radio/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'auto-radio.maps.yandex.net' limit 1; |

## How to fix common problems

- [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
- **Alice** You may use @AmandaJohnsonBot to debug Alice requests in testing.

## Documentation

- [FM-radio](https://wiki.yandex-team.ru/automotive/serverdevelopment/fmradio/)
- [How to update radio data](https://wiki.yandex-team.ru/automotive/serverdevelopment/fmradio/updates/#dannyeiobnovlenija)

## Known clients

- Automotive head-units (autolauncher, autokit, fm-radio application)
- Alice (Megamind)

Service is available to the outer world via automotive [proxy](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/proxy) service. Alice handles are available only from the internal network and the Megamind sends requests directly to the auto-radio balancer.

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_auto_radio) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_auto_radio.py)

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_radio_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_radio_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_radio_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_AUTO_RADIO_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_RADIO_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_AUTO_RADIO_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_RADIO_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations

* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/YCARBACKEND?service=maps-auto-radio
    * Sandbox (line): https://sandbox.yandex-team.ru/scheduler/25175
    * Тикет (line): https://st.yandex-team.ru/YCARBACKEND-453
    * Sandbox (const): https://sandbox.yandex-team.ru/scheduler/25176
    * Тикет (const): https://st.yandex-team.ru/YCARBACKEND-454
