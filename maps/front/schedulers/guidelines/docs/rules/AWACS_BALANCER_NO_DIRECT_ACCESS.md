# AWACS_BALANCER_NO_DIRECT_ACCESS

Awacs balancer must not have any direct access. All access must be inherited from the namespace.

## Reason
It is more convenient manage all access through Awacs namespace.

## Solution
1) Go to the awacs namespace.
2) Select the target top-level balancer from list.
3) Tap "Edit" button in left sidebar.
4) Choose "Auth" tab.
5) Remove all personal logins and ABC groups from the balancer access.

## Autofix
Autofix is available for this rule.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/access.test.ts#L55-77)_
