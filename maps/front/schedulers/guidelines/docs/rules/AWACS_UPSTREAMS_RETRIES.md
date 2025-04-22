# AWACS_UPSTREAMS_RETRIES

Awacs balancer's upstream must have exactly 2 attempts.

## Reason
1 retry can protect from minor network issues/flaps.
However additional retries are less effective, but they generate more rps and encrease timings.

## Solution
Add `attempts: 2` to upstream yaml config in balancer section e.g.:
```yml
l7_upstream_macro:
    flat_scheme:
        balancer:
            attempts: 2
```

Or:
```yml
l7_upstream_macro:
    flat_scheme:
        balancer:
            attempts: 1
            fast_attempts: 2
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/upstream.test.ts#L258-268)_
