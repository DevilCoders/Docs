# Configurations of Nanny services

## What should I know before starting?
[Nanny documentation](https://wiki.yandex-team.ru/jandekspoisk/sepe/nanny/)
[Instances Spec->Containers](https://wiki.yandex-team.ru/jandekspoisk/sepe/nanny/howtos/structured-instancectl-config-how-to/)
[Move to MTN](https://wiki.yandex-team.ru/jandekspoisk/sepe/nanny/howtos/move-to-mtn/)

Before create a new service for Java Application get answers to [these questions](https://wiki.yandex-team.ru/market/administration/new-rtc-service/).  

## What is the latest way to configure a service?
Use [Pipeline](https://tsum.yandex-team.ru/pipe/projects/sre/release/new/rtc-new-service).  
Use MTN.  
Use Instances Spec->Containers.  
Use service templates  
- [Java Application](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_template_service_for_java_iva/)
- [CPP Application](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_template_service_for_common_sas/)
- [NodeJS Application](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_template_service_for_nodejs_vla/)
- [Python Applicaiton](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_template_service_for_python_sas/)

## How-To

### How to build (pack) a service configuration
```
> ya package lilucrm/operator-window/pkg.json
Source root: /Users/d3rp/Projects/arcadia
...
Package version: 3170951
Creating tarball package market-lilucrm-operator-window version 3170951
> ls market-lilucrm-operator-window*
market-lilucrm-operator-window.3170951.tar.gz
>
```

### How to render configuration files
```
> mkdir -p temp && cd temp && tar xf ../market-lilucrm-operator-window.3170951.tar.gz
> ls
bin  conf  data  tmpl
> BSCONFIG_ITAGS="MSK_FOL_MARKET_GURUASSISTANT_PROD a_ctype_production a_dc_fol a_geo_msk a_itype_guruassistant a_line_fol-5 a_metaprj_unknown a_prj_market a_tier_none a_topology_cgset-memory.limit_in_bytes=239075328 a_topology_cgset-memory.low_limit_in_bytes=134217728 a_topology_group-MSK_FOL_MARKET_GURUASSISTANT_PROD a_topology_version-stable-91-r25 cgset_memory_recharge_on_pgfault_1 a_topology_stable-91-r25 enable_hq_report" BSCONFIG_INAME="fol1-0376:24860" BSCONFIG_IPORT="24860" BSCONFIG_IHOST="myhost.yandex.net" BSCONFIG_IDIR="$(pwd)" ~/Projects/arcadia/market/sre/tools/templater/templater
>
```
