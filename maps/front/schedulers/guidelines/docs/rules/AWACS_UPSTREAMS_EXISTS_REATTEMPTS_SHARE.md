# AWACS_UPSTREAMS_EXISTS_REATTEMPTS_SHARE

Awacs balancer's upstream should have reattempts share section.

## Reason
Reattemps during major network issues can take down instances so they should be limited.

## Solution
1) Go to your awacs namespace.
2) Go to upstreams list.
3) Choose the "main" upstream.
4) Add health check to upstream yaml config in balancer section e.g.:
```yml
l7_upstream_macro:
    flat_scheme:
        balancer:
            max_reattempts_share: 0.2
```

{% note info %}

More information you can find on [Wiki](https://wiki.yandex-team.ru/awacs/upstream-easy-mode/#balancer)

{% endnote %}

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/upstream.test.ts#L105-118)_
