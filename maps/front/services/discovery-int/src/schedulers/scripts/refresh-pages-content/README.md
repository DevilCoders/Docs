# refresh-pages-content

Each page contains a lot of information about organizations.
This script write relevant data about organizations.
Also create issue in startrack for checking organization info.

## Reactor

| Environment | URL |
|---|---|
| Testing | https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Ffront%2Fdiscovery-int%2Fschedulers%2Frefresh-pages-content-testing |
| Production | https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Ffront%2Fdiscovery-int%2Fschedulers%2Frefresh-pages-content-production |

## Nirvana Secrets

| Environment | URL |
|---|---|
| Testing | https://nirvana.yandex-team.ru/secret/64380824-1920-465a-96fc-f7078b462790 |
| Production | https://nirvana.yandex-team.ru/secret/5598f610-b430-4f9f-ad0d-df072b62565e |

## Release

Release new binary by running `npm version patch` or `npm version minor` or `npm version major`. This will bump package.json version, build new binary and upload it to remote storage. Then push commit and tag to master: `git push origin master --follow-tags`. Reactor config [will be updated](https://github.yandex-team.ru/maps/infra/tree/master/packages/lama-webhook-parser) every time you push a commit to master.

Read more about binary schedulers [here](https://github.yandex-team.ru/maps/infra/tree/master/packages/bean).
