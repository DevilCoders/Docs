# Core Nmaps Mrc Browser


## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Сухов (quoter@yandex-team.ru) Михаил Плоткин (miplot@yandex-team.ru)|
| Ответственный SRE | Борис Чикунов (chikunov@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/browser/ |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-browser/ |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_BROWSER |
| Release machine | https://rm.z.yandex-team.ru/component/maps_core_nmaps_mrc_browser |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Datatesting | [maps_core_nmaps_mrc_browser_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_browser_datatesting/) | [ core-nmaps-mrc-browser.datatesting ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-browser-datatesting-panel-main/) | [ maps_core_nmaps_mrc_browser_datatesting ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_browser_datatesting) |
| Load | [maps_core_nmaps_mrc_browser_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_browser_load/) | [ core-nmaps-mrc-browser.load ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-browser-load-panel-main/) | [ maps_core_nmaps_mrc_browser_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_browser_load) |
| Prestable | [maps_core_nmaps_mrc_browser_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_browser_prestable/) | [ core-nmaps-mrc-browser.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-browser-prestable-panel-main/) | [ maps_core_nmaps_mrc_browser_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_browser_prestable) |
| Stable | [maps_core_nmaps_mrc_browser_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_browser_stable/) | [ core-nmaps-mrc-browser.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-browser-stable-panel-main/) | [ maps_core_nmaps_mrc_browser_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_browser_stable) |
| Testing | [maps_core_nmaps_mrc_browser_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_browser_testing/) | [ core-nmaps-mrc-browser.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-browser-testing-panel-main/) | [ maps_core_nmaps_mrc_browser_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_browser_testing) |

[Monitorings all (tag=a_prj_maps-core-nmaps-mrc-browser)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-mrc-browser)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Datatesting | common_default | [core-nmaps-mrc-browser.common.datatesting.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.datatesting.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-nmaps-mrc-browser.common.datatesting.maps.yandex.net"}) | [core-nmaps-mrc-browser.common.datatesting.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.datatesting.maps.yandex.net;prj=common.datatesting.maps.yandex.net;signal=core-nmaps-mrc-browser_common_datatesting_maps_yandex_net;) | [rtc_balancer_common_datatesting_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_sas) <br>[rtc_balancer_common_datatesting_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_man) <br>[rtc_balancer_common_datatesting_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_vla) |
| Datatesting | crowdtest | [core-nmaps-mrc-browser-crowdtest.common.datatesting.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.datatesting.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-nmaps-mrc-browser.common.datatesting.maps.yandex.net"}) | [core-nmaps-mrc-browser-crowdtest.common.datatesting.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.datatesting.maps.yandex.net;prj=common.datatesting.maps.yandex.net;signal=core-nmaps-mrc-browser_common_datatesting_maps_yandex_net;) | [rtc_balancer_common_datatesting_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_sas) <br>[rtc_balancer_common_datatesting_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_man) <br>[rtc_balancer_common_datatesting_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_vla) |
| Datatesting | default_ru | [core-nmaps-mrc-browser.common.datatesting.maps.yandex.ru](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.datatesting.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-nmaps-mrc-browser.common.datatesting.maps.yandex.net"}) | [core-nmaps-mrc-browser.common.datatesting.maps.yandex.ru](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.datatesting.maps.yandex.net;prj=common.datatesting.maps.yandex.net;signal=core-nmaps-mrc-browser_common_datatesting_maps_yandex_net;) | [rtc_balancer_common_datatesting_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_sas) <br>[rtc_balancer_common_datatesting_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_man) <br>[rtc_balancer_common_datatesting_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatesting_maps_yandex_net_vla) |
| Stable | default | [core-nmaps-mrc-browser.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-mrc-browser.maps.yandex.net/) | [core-nmaps-mrc-browser.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=vla,sas;fqdn=core-nmaps-mrc-browser.maps.yandex.net;prj=core-nmaps-mrc-browser-maps;signal=service_total;) | [rtc_balancer_core-nmaps-mrc-browser_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-browser_maps_yandex_net_sas) <br>[rtc_balancer_core-nmaps-mrc-browser_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-browser_maps_yandex_net_vla) |
| Stable | internal | [core-nmaps-mrc-browser-internal.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-mrc-browser-internal.maps.yandex.net/) | [core-nmaps-mrc-browser-internal.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=vla,sas;fqdn=core-nmaps-mrc-browser-internal.maps.yandex.net;prj=core-nmaps-mrc-browser-internal-maps;signal=service_total;) | [rtc_balancer_core-nmaps-mrc-browser-internal_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-browser-internal_maps_yandex_net_sas) <br>[rtc_balancer_core-nmaps-mrc-browser-internal_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-browser-internal_maps_yandex_net_vla) |
| Testing | default | [core-nmaps-mrc-browser.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-mrc-browser.testing.maps.yandex.net/) | [core-nmaps-mrc-browser.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas;fqdn=core-nmaps-mrc-browser.testing.maps.yandex.net;prj=core-nmaps-mrc-browser-testing-maps;signal=service_total;) | [rtc_balancer_core-nmaps-mrc-browser_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-mrc-browser_testing_maps_yandex_net_sas) |

## What happens when service is down

Снимки зеркал не показываются в НЯК и БЯК

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/mrc-browser/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : ```SELECT * FROM hahn.`//home/logfeller/logs/maps-log/1d/2019-10-12` WHERE vhost='core-nmaps-mrc-browser.maps.yandex.ru'```; |


## Coredumps

Service's coredumps are collected here: [coredumps.yandex-team.ru](https://coredumps.yandex-team.ru/index?text_to_search=&itype=core-nmaps-mrc-browser&ctype_list=&prj_list=&tag_list=&host_list=&signal=)

## How to fix common problems

### MDS

Handles `GET /feature/$/{image,thumbnail}` load image from MDS. If theirs timings are high or there
are too many `499, 5xx` one should check graphics of MDS proxy for `maps_mrc` namespace: https://yasm.yandex-team.ru/template/panel/mds_proxy/ns=maps_mrc/2/?by=geo . In case of problemds on MDS side report
to their Emergency telegram chat: https://t.me/joinchat/Lz2_8w1qRw7-PDRGLP3b3w

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)


## Known clients
Layer of MRC photos in NMAPS:
| Environment | nmaps | maps | 
| ----------- | --- | --- | 
| Production | [n.maps.yandex.ru](https://n.maps.yandex.ru) | [yandex.ru/maps](https://yandex.ru/maps) | 
| Testing | [nmaps-mrc-testing.tst.c.maps.yandex.ru](https://nmaps-mrc-testing.tst.c.maps.yandex.ru) | [l7test.yandex.ru/maps](https://l7test.yandex.ru/maps/213/moscow/?l=mrc&ll=37.613093%2C55.698285&z=10.3) | 
| Datatesting | [nmaps.tst.maps.yandex.ru](https://nmaps.tst.maps.yandex.ru) | [l7test.yandex.ru/maps?host_config](https://l7test.yandex.ru/maps/213/moscow/?host_config%5Bhosts%5D%5BmrcApi%5D=https%3A%2F%2Fcore-nmaps-mrc-browser.common.datatesting.maps.yandex.net%2F&host_config%5Bhosts%5D%5BmrcHotspotTiles%5D=https%3A%2F%2Fcore-nmaps-mrc-browser.common.datatesting.maps.yandex.net%2Ffeatures%2Fhotspot%3Fl%3Dmrce%26%25c%26&host_config%5Bhosts%5D%5BmrcpeHotspotTiles%5D=https%3A%2F%2Fcore-nmaps-mrc-browser.common.datatesting.maps.yandex.net%2Ffeatures%2Fhotspot%3Fl%3Dmrcpe%26%25c&host_config%5Bhosts%5D%5BmrcpeTiles%5D=https%3A%2F%2Fcore-nmaps-mrc-browser.common.datatesting.maps.yandex.net%2Ftiles%3Fl%3Dmrcpe%26%25c&host_config%5Bhosts%5D%5BmrcTiles%5D=https%3A%2F%2Fcore-nmaps-mrc-browser.common.datatesting.maps.yandex.net%2Ftiles%3Fl%3Dmrce%26%25c&host_config%5Binthosts%5D%5BmrcApi%5D=http%3A%2F%2Fcore-nmaps-mrc-browser.common.datatesting.maps.yandex.net%2F&host_config%5Binthosts%5D%5BmrcpeStamp%5D=http%3A%2F%2Fcore-nmaps-mrc-browser.common.datatesting.maps.yandex.net%2Ffeatures%2FstampPedestrian.xml&host_config%5Binthosts%5D%5BmrcStamp%5D=http%3A%2F%2Fcore-nmaps-mrc-browser.common.datatesting.maps.yandex.net%2Ffeatures%2Fstamp.xml&ll=37.622504%2C55.753215&z=10) | 


## Ecstatic Datasets
| Stable | Testing | Datatesting |
| ------ | ------- | ----------- |
| [yandex-maps-coverage5-geoid](http://ecstatic.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) | [yandex-maps-coverage5-geoid](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) | [yandex-maps-coverage5-geoid](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) |
| [yandex-maps-mrc](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc/versions) | [yandex-maps-mrc](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc/versions) | [yandex-maps-mrc](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc/versions) |
| [yandex-maps-mrc-activation](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-activation/versions) | [yandex-maps-mrc-activation](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-activation/versions) | [yandex-maps-mrc-activation](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-activation/versions) |
| [yandex-maps-mrc-design](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-design/versions) | [yandex-maps-mrc-design](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-design/versions) | [yandex-maps-mrc-design](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-design/versions) |
| [yandex-maps-mrc-graph](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-graph/versions) | [yandex-maps-mrc-graph](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-graph/versions) | [yandex-maps-mrc-graph](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-graph/versions) |
| [yandex-maps-mrc-pedestrian-graph](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph/versions) | [yandex-maps-mrc-pedestrian-graph](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph/versions) | [yandex-maps-mrc-pedestrian-graph](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph/versions) |
| [yandex-maps-mrc-photo-to-edge](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-edge/versions) | [yandex-maps-mrc-photo-to-edge](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-edge/versions) | [yandex-maps-mrc-photo-to-edge](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-edge/versions) |
| [yandex-maps-mrc-photo-to-pedestrian-edge](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-pedestrian-edge/versions) | [yandex-maps-mrc-photo-to-pedestrian-edge](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-pedestrian-edge/versions) | [yandex-maps-mrc-photo-to-pedestrian-edge](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-pedestrian-edge/versions) |
## SLA
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_nmaps_mrc_browser?scale=d&_period_distance=30&_incl_fields=d1&_incl_fields=d30&_incl_fields=d7) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_nmaps_mrc_browser.py)


## Persistent Volumes
* /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log


## How to run in development environment

1. Build `ya make`

2. Copy wiki-config `/etc/yandex/maps/wiki/services/yav-deploy/templates/{environment}.conf` from RTC service.

3. Download required ecstatic datasets:
    - yandex-maps-coverage5-geoid
    - yandex-maps-mrc
    - yandex-maps-mrc-design
    - yandex-maps-mrc-graph
    - yandex-maps-mrc-pedestrian-graph
    - yandex-maps-mrc-photo-to-edge
    - yandex-maps-mrc-photo-to-pedestrian-edge

    ```
    export ENVIRONMENT_NAME=stable
    for dataset in yandex-maps-coverage5-geoid \
                   yandex-maps-mrc \
                   yandex-maps-mrc-design \
                   yandex-maps-mrc-graph \
                   yandex-maps-mrc-pedestrian-graph \
                   yandex-maps-mrc-photo-to-edge \
                   yandex-maps-mrc-photo-to-pedestrian-edge; do
        ecstatic download `ecstatic versions $dataset | head -n1`;
    done
    ```

4. Run instance:
    ```
    YCR_MODE=fastcgi:/var/run/yandex/maps/yacare/mrc-browser.sock ./mrc-browser \
        --config ../../libs/config/cfg/t-config.production.xml \
        --wiki-config wiki-config.xml \
        --secret-version sec-01fjesdh3jykc9s87detcnw9mr \
        --graph_dir yandex-maps-mrc-graph_dir \
        --pedestrian_graph_dir yandex-maps-mrc-pedestrian-graph_dir \
        --photo_to_edge_dir yandex-maps-mrc-photo-to-edge_dir \
        --photo_to_pedestrian_edge_dir yandex-maps-mrc-photo-to-pedestrian-edge_dir \
        --geoid_coverage_path yandex-maps-coverage5-geoid_dir \
        --mrc-data-dir yandex-maps-mrc_dir \
        --design_dir yandex-maps-mrc-design \
        --icons_dir ../icons/ \
        --disable-tvm
    ```

5. Run command:
    ```
    chmod a+rwx /var/run/yandex/maps/yacare/mrc-browser.sock
    ```

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NMAPS_MRC_BROWSER_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MRC_BROWSER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NMAPS_MRC_BROWSER_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MRC_BROWSER_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSMRC?service=maps-core-nmaps-mrc-browser
    * Sandbox: https://sandbox.yandex-team.ru/schedulers/?tags=YANDEX-MAPS-WIKI-MRC-BROWSER-LOAD-TESTING
    * Semaphore: https://sandbox.yandex-team.ru/admin/semaphores/16166380/view
    * Тикет: https://st.yandex-team.ru/MAPSMRC-171
