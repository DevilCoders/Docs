# Core Stv Preview

Превью или static api для панорам

Для id панорамы и направлению отдает картинку с участком панорамы.

Подробнее АПИ https://wiki.yandex-team.ru/maps/dev/core/streetview/stv-preview/

Для рендеринга скачивает тайлы из s3 mds.
Чтобы понять какие тайлы скачивать и как их склеивать используем датасет для описаний панорам.

Задача в рамках которой делался сервис. Можно понять почему некоторые решения сделанны именно так.
https://st.yandex-team.ru/MAPSPANO-458


## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Иванов (idg@yandex-team.ru) <br> Игорь Орпанен (orphean@yandex-team.ru) |
| Отвественные SRE | Дмитрий Иванов (idg@yandex-team.ru) <br> Игорь Орпанен (orphean@yandex-team.ru) |
| Исходники | [maps/streetview/preview](https://a.yandex-team.ru/arc/trunk/arcadia/maps/streetview/preview) |
| Сервис в ABC | [maps-core-stv-preview](https://abc.yandex-team.ru/services/maps-core-stv-preview/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_STV_PREVIEW |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Load | [maps_core_stv_preview_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_preview_load/) | [ core-stv-preview.load ](https://yasm.yandex-team.ru/template/panel/maps-core-stv-preview-load-panel-main/) | [ maps_core_stv_preview_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_stv_preview_load) |
| Prestable | [maps_core_stv_preview_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_preview_prestable/) | [ core-stv-preview.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-stv-preview-prestable-panel-main/) | [ maps_core_stv_preview_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_stv_preview_prestable) |
| Stable | [maps_core_stv_preview_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_preview_stable/) | [ core-stv-preview.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-stv-preview-stable-panel-main/) | [ maps_core_stv_preview_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_stv_preview_stable) |
| Testing | [maps_core_stv_preview_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_preview_testing/) | [ core-stv-preview.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-stv-preview-testing-panel-main/) | [ maps_core_stv_preview_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_stv_preview_testing) |


[Monitorings all (tag=a_prj_maps-core-stv-preview)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-stv-preview)



### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [static-pano.maps.yandex.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/static-pano.maps.yandex.ru/) | [static-pano.maps.yandex.ru](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=static-pano.maps.yandex.ru;itype=balancer;ctype=prod;locations=sas,vla,man;prj=core-stv-preview-maps;signal=service_total) | [rtc_balancer_static-pano_maps_yandex_ru_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_static-pano_maps_yandex_ru_man)<br>[rtc_balancer_static-pano_maps_yandex_ru_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_static-pano_maps_yandex_ru_sas)<br>[rtc_balancer_static-pano_maps_yandex_ru_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_static-pano_maps_yandex_ru_vla) |


## What happens when service is down

Перестают подгружаться превью сниппетов панорам в карточках топонимов

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/stv_preview/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2020-03-15` WHERE vhost LIKE 'static-pano.maps.yandex.ru' limit 1; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Написать в чат поддержки "MDS/Avatars/S3 emergency" при невозможности загрузить тайлы
Откатить датасет экстатика yandex-maps-streetview-description


## Documentation

Описание того что хотели сделать 
https://st.yandex-team.ru/MAPSPANO-458
АПИ https://wiki.yandex-team.ru/maps/dev/core/streetview/stv-preview/

## Known clients
БЯК - в случае поломки не будут подгружаться превью для сниппетов панорам. Пользователь будет видеть заглушку вместо сниппета.
Недвижимость - пока не используют, только собираются.

## Ecstatic Datasets

| Stable | Testing |
| ------ | ------- |
| [yandex-maps-streetview-description](http://ecstatic.maps.yandex.net/pkg/yandex-maps-streetview-description/versions) | [yandex-maps-streetview-description](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-streetview-description/versions) |


## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_stv_preview) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_stv_preview.py)


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Load | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_preview_load/yp_pods/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_preview_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_preview_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_stv_preview_testing/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_STV_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_STV_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_STV_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_STV_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSPANO
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/19265
    * Тикет: https://st.yandex-team.ru/MAPSPANO-463

