# AWACS_XFFY_HEADER

## Reason
You need to use l7_macro version 0.3.x and higher in top_level config.

## Solution
For **External balancer** it should look something like this:
```yaml
l7_macro:
  version: 0.3.10
  core: {}
```

For **Internal balancer** it should look something like this:
```yaml
 l7_macro:
   version: 0.3.10
   core:
     trust_x_forwarded_for_y: true
```

1. Go To [AWACS](https://nanny.yandex-team.ru/ui/#/awacs/)
1. Select your balancer
1. Open "top_level" config
1. Check the configuration of the section

{% note info %}

* **External balancer** - these are load balancers that external users go to directly
* **Internal balancer** - these are balancers that either other Yandex services go to, or strictly internal Yandex users

If you don't know which balancer you have, check with the [duty DevOps](https://abc.yandex-team.ru/services/maps-front/?scope=dutywork)

{% endnote %}

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/top-level.test.ts#L137-149)_
