# B2Bgeo Pipedrive Gate

Gateway to pipedrive.com, support new companies & users registration

## General information
| What | Who |
| ---- | --- |
| Сервис в ABC | [maps-b2bgeo-pipedrive-gate](https://abc.yandex-team.ru/services/maps-b2bgeo-pipdrive-gate/)|
| DockerBuild (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_B2BGEO_PIPEDRIVE_GATE |

## Deploy process
1. After each commit testenv builds docker image (link [here](#general-information])).
When it's ready you will receive email from sandbox.
2. When docker image ready check it with `ya tool sedem release info maps/b2bgeo/pipedrive_gate`.
3. Now you can deploy any from `Release candidates` to testing with `ya tool sedem release start maps/b2bgeo/pipedrive_gate r7522292`
    (`r7522292` here for example, choose one from your `Release candidates`).
4. Сheck tests [here](https://testenv.yandex-team.ru/?screen=jobs&database=b2bgeo)
5. If all is ok `ya tool sedem release step maps/b2bgeo/pipedrive_gate v2.1 stable` as example for `v2.1` version,
get your version from `ya tool sedem release info maps/b2bgeo/pipedrive_gate` testing stage.
6. You are perfect!

Detailed documentation about sedem release process can be found [here](https://docs.yandex-team.ru/sedem/releases)

## Forms
### Testing
https://forms.yandex-team.ru/ext/admin/10018222/notifications

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_b2bgeo_pipedrive_gate_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_pipedrive_gate_stable/) | [ b2bgeo-pipedrive-gate.stable ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-pipedrive-gate-stable-panel-main/) | [ maps_b2bgeo_pipedrive_gate_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_pipedrive_gate_stable) |
| Testing | [maps_b2bgeo_pipedrive_gate_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_pipedrive_gate_testing/) | [ b2bgeo-pipedrive-gate.testing ](https://yasm.yandex-team.ru/template/panel/maps-b2bgeo-pipedrive-gate-testing-panel-main/) | [ maps_b2bgeo_pipedrive_gate_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_b2bgeo_pipedrive_gate_testing) |


[Monitorings all (tag=a_prj_maps-b2bgeo-pipedrive-gate)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-b2bgeo-pipedrive-gate)


## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Pycare service | /var/log/yandex/maps/pipedrive_gate/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |


## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

[B2Bgeo Troubleshooting](https://wiki.yandex-team.ru/b2bgeo/dev/helpdesk/troubleshooting/)


## Documentation

https://wiki.yandex-team.ru/b2bgeo/dev/Pipedrive-Gate-Forms/


## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_pipedrive_gate_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_b2bgeo_pipedrive_gate_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_B2BGEO_PIPEDRIVE_GATE_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_PIPEDRIVE_GATE_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_B2BGEO_PIPEDRIVE_GATE_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_B2BGEO_PIPEDRIVE_GATE_TESTING_RTC_NETS_ ) |
