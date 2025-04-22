# Market UGC daemon

## Documentation

## Services
[Service Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_ugcdaemon/)
Services Balancer(testing): [marketugc-testing.n.yandex-team.ru](https://marketugc-testing.n.yandex-team.ru)
Services Balancer(production):

## Sandbox tasks
### Build tasks
[MARKET_YA_MAKE](https://sandbox.yandex-team.ru/tasks/?order=-updated&type=MARKET_YA_MAKE) with the following options:

- Svn url for arcadia: arcadia:/arc/trunk/arcadia@%COMMITNUMBER_FROM_ARCADIA%
- Build artifacts: market/tarantino/tarantino-server/market-tarantino-bin: [MARKET_UGCDAEMON_BIN](https://sandbox.yandex-team.ru/resources/?type=MARKET_UGCDAEMON_BIN)
- Build system: ya
- Build type: release
- Check "ya make" return code: True

[Example: https://sandbox.yandex-team.ru/task/82320937/view](https://sandbox.yandex-team.ru/task/82320937/view)

### Update service
Go to [Service Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_ugcdaemon/)
Click "resource" pop-up -> choose "market-ugc-daemon" -> click "Edit Resource" -> Task type "MARKET_YA_MAKE" -> Task id "id from MARKET_YA_MAKE TASK" -> Resource type "MARKET_UGCDAEMON_BIN"

### Auxiliary tasks
[BUILD_MARKET_SERVICE_CONFIG](https://sandbox.yandex-team.ru/tasks/?order=-updated&type=BUILD_MARKET_SERVICE_CONFIG) with the following options:

- Svn url for arcadia:  arcadia:/arc/trunk/arcadia@2603291  (where 2603291 commit to https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/nanny/comments/ugc)
- Service path:  /market/sre/nanny/comments/ugc 
- Release service: True
- Service IDs with environment:  testing_ugc_daemon_sas: testing
								 testing_ugc_daemon_man: testing
								 testing_ugc_daemon_msk: testing

[Example: https://sandbox.yandex-team.ru/task/82041676/view](https://sandbox.yandex-team.ru/task/82041676/view)

[BUILD_TEMPLATER](https://sandbox.yandex-team.ru/tasks/?order=-updated&type=BUILD_TEMPLATER)

just use as is

[Example: https://sandbox.yandex-team.ru/task/78813281/view](https://sandbox.yandex-team.ru/task/78813281/view)

## Dashboards
[HQ Panel](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_ugcdaemon/hq-panel/)
