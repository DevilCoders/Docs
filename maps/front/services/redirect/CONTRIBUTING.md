## Description
Репозиторий сделан по правилам монорепы, архитектура описана на [WiKi](https://wiki.yandex-team.ru/search-interfaces/monorepo/howto/#strukturarepozitorija)

## How to release?

Recommended:

1. `npm i`
2. `npx qtools tag patch`
3. `npx qtools release production --manual`
4. check all in prestable
5. activate all other instances


## Add new redirect/Domain

1. Add domain in `qtools.json`
2. Deploy to production
3. Change certificate type in UI to production (CertumProductionCA)
4. Wait for the SECTASK to be resolved and closed
5. Add DNS record by dns-monkey if domain contains `*.maps.yandex.*` or dns.tt.yandex-team.ru if not. More [details](https://wiki.yandex-team.ru/maps/dev/ui/deploy/devops/#dns)
