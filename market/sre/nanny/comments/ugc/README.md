# Market UGC daemon

## Documentation

## Services
[Service Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_ugcdaemon/)
Services Balancer(testing): [marketugc-testing.n.yandex-team.ru](https://marketugc-testing.n.yandex-team.ru)
Services Balancer(production):

## Sandbox tasks
### Build tasks
[MARKET_YA_PACKAGE](https://sandbox.yandex-team.ru/tasks/?order=-updated&type=MARKET_YA_PACKAGE) with the following options:

- Svn url for arcadia: arcadia:/arc/trunk/arcadia@%COMMITNUMBER_FROM_ARCADIA%
- Build artifacts: market/ugc/daemon/market-ugc-daemon: [MARKET_UGCDAEMON](https://sandbox.yandex-team.ru/resources/?type=MARKET_UGCDAEMON)
- Build system: ya
- Build type: release
- Check "ya make" return code: True

[Example: https://sandbox.yandex-team.ru/task/89282784/view](https://sandbox.yandex-team.ru/task/89282784/view)


## Dashboards
[HQ Panel](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_ugcdaemon/hq-panel/)
