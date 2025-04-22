# yns
> An ycg-like tool for resolving Nanny service to hostnames

## Build

```
> ya make --checkout market/sre/tools/yns
```

## Usage example

```
> market/sre/tools/yns/yns --help
Usage: yns [OPTIONS] SERVICE_NAME...

Options:
  --with-state             Add state of container.
  --with-port              Add port to hostname.
  --use-container BOOLEAN  Get container_hostname instead of hostname.
  --version                Show the version and exit.
  --help                   Show this message and exit.
>
> market/sre/tools/yns/yns testing_market_carter_sas
sas2-3195-sas-market-test-carter-22485.gencfg-c.yandex.net
sas2-1747-sas-market-test-carter-22485.gencfg-c.yandex.net
>
> market/sre/tools/yns/yns testing_market_carter_sas testing_market_carter_vla
sas2-1747-sas-market-test-carter-22485.gencfg-c.yandex.net
sas2-3195-sas-market-test-carter-22485.gencfg-c.yandex.net
vla1-5743-vla-market-test-carter-22495.gencfg-c.yandex.net
vla1-5744-vla-market-test-carter-22495.gencfg-c.yandex.net
>
> market/sre/tools/yns/yns testing_market_front_desktop_sas --use-container=false
Attention! Hostnames of host machines will be printed instead of hostnames of containers
sas1-2415.search.yandex.net
sas1-2414.search.yandex.net
>
> market/sre/tools/yns/yns production_market_classifier_sas production_market_classifier_vla --with-port
sas3-1120-f49-sas-market-prod--495-18974.gencfg-c.yandex.net 18974
sas3-1121-c7d-sas-market-prod--495-18974.gencfg-c.yandex.net 18974
sas3-1123-3ff-sas-market-prod--495-18974.gencfg-c.yandex.net 18974
sas3-1124-6f4-sas-market-prod--495-18974.gencfg-c.yandex.net 18974
vla1-5934-vla-market-prod-clas-90a-29570.gencfg-c.yandex.net 29570
vla1-5936-vla-market-prod-clas-90a-29570.gencfg-c.yandex.net 29570
vla1-5937-vla-market-prod-clas-90a-29570.gencfg-c.yandex.net 29570
vla1-5939-vla-market-prod-clas-90a-29570.gencfg-c.yandex.net 29570
>
> market/sre/tools/yns/yns production_market_classifier_sas production_market_classifier_vla --with-state
sas3-1120-f49-sas-market-prod--495-18974.gencfg-c.yandex.net ACTIVE->ACTIVE
sas3-1121-c7d-sas-market-prod--495-18974.gencfg-c.yandex.net ACTIVE->ACTIVE
sas3-1123-3ff-sas-market-prod--495-18974.gencfg-c.yandex.net ACTIVE->ACTIVE
sas3-1124-6f4-sas-market-prod--495-18974.gencfg-c.yandex.net ACTIVE->ACTIVE
vla1-5934-vla-market-prod-clas-90a-29570.gencfg-c.yandex.net ACTIVE->ACTIVE
vla1-5936-vla-market-prod-clas-90a-29570.gencfg-c.yandex.net ACTIVATED_INSTANCE_DYNAMIC_RESOURCES_NOT_READY->ACTIVE
vla1-5937-vla-market-prod-clas-90a-29570.gencfg-c.yandex.net ACTIVE->ACTIVE
vla1-5939-vla-market-prod-clas-90a-29570.gencfg-c.yandex.net PREPARED->PREPARED
>
```

## Links

https://wiki.yandex-team.ru/jandekspoisk/sepe/nanny/service-repo-api/#current-service-instances
