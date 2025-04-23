# AWACS_BALANCING_SCHEME

If a service has less than four pods in each DC then its upstreams should be configured with flat balancing scheme.
If a service has more than three pods in each DC then its upstreams should be configured with geo balancing scheme.

## How to Fix

1. If a service has no 'production' stage in YDeploy, please create one.
2. If a service has more than three pods in each DC in production stage, please add 'by_dc_scheme' key
to the configuration of corresponding upstreams. And vice versa, if a service has less than four pods
in each DC in production stage, please add 'flat_scheme' key to the configuration of corresponding upstreams.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/balancing-scheme.test.ts#L22-46)_
