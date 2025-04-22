# AWACS_UPSTREAMS_EXISTS_PESSIMIZED_ENDPOINTS_SHARE

Awacs balancer's upstream should have pessimized endpoints share section.

## Reason
Awacs will ignore health checks if the share of unavailable endpoints greater than this value.
It should be 1.0, but the maximum value allowed by awacs is 0.5.

## Solution
1) Go to your awacs namespace.
2) Go to upstreams list.
3) Choose the "main" upstream.
4) Add health check to upstream yaml config in balancer section e.g.:
```yml
l7_upstream_macro:
    flat_scheme:
        balancer:
            max_pessimized_endpoints_share: 0.5
```

{% note info %}

More information you can find on [Wiki](https://wiki.yandex-team.ru/awacs/upstream-easy-mode/#balancer)

{% endnote %}

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/upstream.test.ts#L146-159)_
