# AWACS_UPSTREAMS_EXISTS

Awacs balancer should have specific list of upstreams.

## Reason
For unification and separation of concerns.

## Solution
1) Go to your awacs namespace.
2) Go to upstreams list.
3) Check actual upstreams list with required, witch contains: `main, default`.

{% note info %}

Each type of upstream designed for a specific purpose:
- `main` - uses for base logic of your balancer
- `default` - serves as a handler in case the previous upstreams did not process the request. It should be latest in upstreams order and have field `matcher.any: true`. Example config:
    ```yml
    l7_upstream_macro:
        version: 0.0.1
        id: default
        matcher:
            any: true
        static_response:
            status: 421
            content: Misdirected Request
    ```

{% endnote %}

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/upstream.test.ts#L53-78)_
