# market-deploy-nginx-juggler-bundle

Бандл с проверками для бокса с nginx для сервисов в Y.Deploy.

## Документация
### Сборка в виде juggler-bundle
* [Сборка бандла](https://docs.yandex-team.ru/juggler/client/bundles#how-to-build). Сборка выполняется из файла bundle.json.
* [Добавление бандла в deploy](https://wiki.yandex-team.ru/deploy/docs/concepts/pod/sidecars/jugglersubagent/)

### Сборка в виде слоя
* Сборка выполняется таской MARKET_YA_PACKAGE.
* Сборка выполняется из файла pkg.json.

## Проверки в бандле
* [nginx-status](https://a.yandex-team.ru/arc_vcs/market/sre/juggler/bundles/checks/nginx-status/)
