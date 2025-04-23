# market-deploy-app-juggler-bundle

Бандл с проверками для бокса с приложением для сервисов в Y.Deploy.

## Документация
### Сборка в виде juggler-bundle
* [Сборка бандла](https://docs.yandex-team.ru/juggler/client/bundles#how-to-build). Сборка выполняется из файла bundle.json.
* [Добавление бандла в deploy](https://wiki.yandex-team.ru/deploy/docs/concepts/pod/sidecars/jugglersubagent/)

### Сборка в виде слоя
* Сборка выполняется таской MARKET_YA_PACKAGE.
* Сборка выполняется из файла pkg.json.

## Проверки в бандле
* [memory_anon_usage](https://a.yandex-team.ru/arc_vcs/market/sre/juggler/bundles/checks/memory_anon_usage/)
* [logrotate-app](https://a.yandex-team.ru/arc_vcs/market/sre/juggler/bundles/checks/shell/logrotate/)
* [data-getter-freshness](https://a.yandex-team.ru/arc_vcs/market/sre/juggler/bundles/checks/data_getter_freshness/)
