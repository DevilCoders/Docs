stage specs
===========

This directory contents:
1. `base` - common service settings: computing resources requests, common environment variables and files
2. `dev`, `pre`, `prod` - settings specific for each of the stages - dev secrets for dev stage, prod secrets for prod, etc.
3. `{dev,pre,prod}/infra.{dev,pre,prod}.yaml` - rendered stages (merged from `base` and `dev`, `pre`, `prod`)

For details see [docs](https://docs.yandex-team.ru/infractl/howto).
