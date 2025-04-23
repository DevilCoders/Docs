# AWACS_UPSTREAM_NO_DIRECT_ACCESS

Awacs upstream must not have any direct access. All access must be inherited from the namespace.

## Reason
It is more convenient manage all access through Awacs namespace.

## Solution
1) Go to the awacs namespace upstreams.
2) Select the target upstream from the list.
3) Tap "Edit" button in left sidebar.
4) Choose "Auth" tab.
5) Remove all personal logins and ABC groups from the upstream access.

## Autofix
Autofix is available for this rule.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/access.test.ts#L96-118)_
