# AWACS_TOP_LEVEL_HEADERS_EXIST

## Reason
All our services should have the necessary minimum of standard headers

## Solution
For **External balancer** it should look something like this in top_level config:
```yaml
 headers:
   - create: {target: X-Forwarded-For, func: realip}
   - create: {target: X-Forwarded-Host, func: host}
   - create: {target: X-Forwarded-Proto, func: scheme}
   - create: {target: X-Real-IP, func: realip}
   - create: {target: X-Req-Id, func: reqid}
   - create: {target: X-Source-Port-Y, func: realport}
```

For **Internal balancer** it should look something like this:
```yaml
 headers:
   - create: {target: X-Forwarded-For, keep_existing: true, func: realip}
   - create: {target: X-Forwarded-Host, keep_existing: true, func: host}
   - create: {target: X-Forwarded-Proto, keep_existing: true, func: scheme}
   - create: {target: X-Real-IP, keep_existing: true, func: realip}
   - create: {target: X-Req-Id, keep_existing: true, func: reqid}
   - create: {target: X-Source-Port-Y, keep_existing: true, func: realport}
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
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/top-level.test.ts#L84-100)_
