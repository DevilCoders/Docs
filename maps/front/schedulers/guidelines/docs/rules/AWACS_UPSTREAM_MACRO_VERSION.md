# AWACS_UPSTREAM_MACRO_VERSION

Awacs balancer's L7 upstream macro version must be at least 0.2.3

## Reason
This is the last recommended version by Awacs team.

## Solution
Set `l7_upstream_macro.version` parameter to "0.2.3".

```yml
l7_upstream_macro:
    version: 0.2.3
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/upstream.test.ts#L285-298)_
