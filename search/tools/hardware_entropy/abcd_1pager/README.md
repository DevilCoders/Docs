# ABCD 1pager generator

## Input data

- `.abc_token`: file with OAuth token for ABC
- `.dispenser_token`: OAuth token for Dispenser
- `bot-hwr-pre-orders.csv` and `bot-hwr-upgrades.csv` (downloaded from keyd@)
- `requests_servers_without_reserves.csv`: file obtained via [ABC export](https://abc.yandex-team.ru/dispenser/common/api/v1/quota-requests/export/csv?campaignOrder=7&campaignOrder=8&campaignOrder=9&status=READY_FOR_REVIEW&status=CONFIRMED&sortBy=UPDATED_AT&sortOrder=DESC&page=1&servers=true&withoutReserves=true)
- `requests_servers.csv`: file obtained via [ABC export](https://abc.yandex-team.ru/dispenser/common/api/v1/quota-requests/export/csv?campaignOrder=7&campaignOrder=8&campaignOrder=9&status=READY_FOR_REVIEW&status=CONFIRMED&sortBy=UPDATED_AT&sortOrder=DESC&page=1&servers=true)

## How to use
- Download necessary files and obtain tokens
- Run `./run.sh` to generate 1pagers and pivot

