# AWACS_UPSTREAMS_HEALTH_CHECK

Awacs balancer's upstream should have health check section.

## Reason
Health check section difines how balancer can identify if endpoint alive or not.

## Solution
1) Go to your awacs namespace.
2) Go to upstreams list.
3) Choose the "main" upstream.
4) Add health check to upstream yaml config in balancer section for example.slb.maps.yandex.net namespace e.g.:
```yml
l7_upstream_macro:
    flat_scheme:
        balancer:
            health_check:
            delay: 5s
            request: >-
                GET /ping HTTP/1.1\nHost:
                example.slb.maps.yandex.net\nUser-agent: l7-balancer\n\n
```

{% note info %}

More information you can find on [Wiki](https://wiki.yandex-team.ru/awacs/upstream-easy-mode/#balancer)

{% endnote %}

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/upstream.test.ts#L190-201)_
