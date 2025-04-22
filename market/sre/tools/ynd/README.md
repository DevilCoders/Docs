# ynd
> An ycg-like tool for resolving Nanny dashboard to services

## Build

```
> ya make --checkout market/sre/tools/ynd
```

## Usage example

```
> market/sre/tools/ynd/ynd --help
Usage: ynd [OPTIONS] DASHBOARD...

Options:
  --use-url      Show URLs instead of service names.
  --with-state   Add states of service.
  --group TEXT  Specify the group of services.
  --list-groups  List groups. It is only possible to get groups of one
                dashboard only.
  --version     Show the version and exit.
  --help        Show this message and exit.
>
> market/sre/tools/ynd/ynd market_classifier 
testing_market_classifier_sas
testing_market_classifier_iva
testing_market_classifier_helper_iva
production_market_classifier_api_sas
production_market_classifier_api_vla
production_market_classifier_helper_sas
production_market_classifier_iva
production_market_classifier_sas
production_market_classifier_vla
>
> market/sre/tools/ynd/ynd market_classifier --list-groups
testing
stable
>
> market/sre/tools/ynd/ynd market_classifier --group stable
production_market_classifier_api_sas
production_market_classifier_api_vla
production_market_classifier_helper_sas
production_market_classifier_iva
production_market_classifier_sas
production_market_classifier_vla
>
> market/sre/tools/ynd/ynd market_classifier --with-state
testing_market_classifier_sas ONLINE
testing_market_classifier_iva ONLINE
testing_market_classifier_helper_iva ONLINE
production_market_classifier_api_sas OFFLINE
production_market_classifier_api_vla OFFLINE
production_market_classifier_helper_sas OFFLINE
production_market_classifier_iva OFFLINE
production_market_classifier_sas OFFLINE
production_market_classifier_vla OFFLINE
>
> market/sre/tools/ynd//ynd market_classifier --group testing --use-url
https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_classifier_sas/
https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_classifier_iva/
https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_classifier_helper_iva/
>
```

## Links

https://wiki.yandex-team.ru/jandekspoisk/sepe/nanny/service-repo-api/#current-service-instances
