# AWACS_NAMESPACE_ONLY_DEVOPS_ACCESS

Awacs namespace must have access only for duty service, no personal access.

## Reason
Dutywork group must have access for all namespaces for solving problems if it is needed.

## Solution
1) Go to the your awacs namespace.
2) Tap "Edit namespace" button in left sidebar.
3) Remove all personal access from namespace.
4) Add ["DevOps (Инфраструктура фронтенда геосервисов)"](https://abc.yandex-team.ru/services/maps-front-infra/?scope=devops) group to namespace access list in "Owners" section.
5) Also add "DevOps" group from your ABC service.

## Autofix
Autofix is available for this rule.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/access.test.ts#L137-160)_
