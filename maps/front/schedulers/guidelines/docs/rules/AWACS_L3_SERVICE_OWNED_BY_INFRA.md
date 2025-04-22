# AWACS_L3_SERVICE_OWNED_BY_INFRA

Awacs L3 service should be owned by maps-front-infra.

## Reason
Infrastructure group must have access L3 service for solving problems if it is needed.

## Solution
You have to add ["DevOps (Инфраструктура фронтенда геосервисов)"](https://abc.yandex-team.ru/services/maps-front-infra/?scope=devops) group to L3 service access list.
If you have not access for this, please contact with actual responsible for duty: ["DevOps (Инфраструктура фронтенда геосервисов"](https://abc.yandex-team.ru/services/maps-front-infra/?scope=devops)

{% note info %}

See more documentation on https://wiki.yandex-team.ru/awacs/certs/

{% endnote %}

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/l3-service.test.ts#L48-55)_
