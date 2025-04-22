# DEPLOY_DEVOPS_ACCESS

Requires access for duty DevOps team.

## Rationale
We have a special DevOps team which watches closely for all our services at nights and holidays. To fix incidents they should have an extra permissions for all services. That's why not only maintainers but DevOps team must have the same accesses.

## Solution
1. Go to your deploy project.
1. Tap "Manage Roles" link in "General access" section.
1. You will be moved to IDM.
1. Tap "Запросить роль" button in header.
1. Fill in first field with value `Я.Деплой > YOUR_ABC_SLUG > OWNER`.
1. Fill in second field with value `maps-front-infra_devops` of group ["DevOps (Инфраструктура фронтенда геосервисов)"](https://abc.yandex-team.ru/services/maps-front-infra/?scope=devops).

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/access.test.ts#L55-64)_
