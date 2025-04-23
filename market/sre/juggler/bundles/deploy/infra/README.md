# market-deploy-infra-juggler-bundle

Бандл с проверками для infa_box для сервисов в Y.Deploy.

## Документация
### Сборка в виде juggler-bundle
* [Сборка бандла](https://docs.yandex-team.ru/juggler/client/bundles#how-to-build). Сборка выполняется из файла bundle.json.
* [Добавление бандла в deploy](https://wiki.yandex-team.ru/deploy/docs/concepts/pod/sidecars/jugglersubagent/)

### Сборка в виде слоя
* Сборка выполняется таской MARKET_YA_PACKAGE.
* Сборка выполняется из файла pkg.json.

## Проверки в бандле
* [push-client-status](https://a.yandex-team.ru/arc_vcs/market/sre/juggler/bundles/checks/shell/push-client/)
* [logrotate](https://a.yandex-team.ru/arc_vcs/market/sre/juggler/bundles/checks/shell/logrotate/)
* [fresh-hprof-files](https://a.yandex-team.ru/arc_vcs/market/sre/juggler/bundles/checks/fresh-hprof-files/)
* [fresh-core-dumps](https://a.yandex-team.ru/arc_vcs/market/sre/juggler/bundles/checks/fresh-core-dumps/)
* [yadi-os](https://a.yandex-team.ru/arc_vcs/market/sre/juggler/bundles/checks/yadi-os/)
* [disk_free_space](https://a.yandex-team.ru/arc_vcs/market/sre/juggler/bundles/checks/pythonic/checks/disk_free_space/)
* [ping](https://a.yandex-team.ru/arc_vcs/market/sre/juggler/bundles/checks/pythonic/checks/ping/)
