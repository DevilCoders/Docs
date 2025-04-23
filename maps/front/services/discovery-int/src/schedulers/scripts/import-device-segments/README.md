# import-device-segments

Clear old device segments from Postgres DB.

## Reactor

| Environment | URL |
|---|---|
| Testing | https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Ffront%2Fdiscovery-int%2Fschedulers%2Fimport-device-segments-testing |
| Production | https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Ffront%2Fdiscovery-int%2Fschedulers%2Fimport-device-segments-production |

## Nirvana Secrets

| Environment | URL |
|---|---|
| Testing | https://nirvana.yandex-team.ru/secret/64380824-1920-465a-96fc-f7078b462790 |
| Production | https://nirvana.yandex-team.ru/secret/5598f610-b430-4f9f-ad0d-df072b62565e |

## Release

Release new binary by running `npm version patch` or `npm version minor` or `npm version major`. This will bump package.json version, build new binary and upload it to remote storage. Then push commit to trunk. Reactor config [will be updated](https://a.yandex-team.ru/arcadia/maps/front/tools/lama-webhook-parser) every time you push a commit to master.

Read more about binary schedulers [here](https://a.yandex-team.ru/arcadia/maps/front/packages/bean).
