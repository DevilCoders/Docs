# AWACS_UPSTREAM_RETRY_NON_IDEMPOTENT_DISABLED

Awacs balancer's upstream must have disabled nonidempotent retries.

## Reason
Nonidempotent reties can cause unpredicted behaviors.
By default they are enabled in awacs, so you should explicitly disable it.

## Solution
Add `retry_non_idempotent: false` to upstream yaml config in balancer section e.g.:
```yml
l7_upstream_macro:
    flat_scheme:
        balancer:
            retry_non_idempotent: false
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/upstream.test.ts#L220-230)_
