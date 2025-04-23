# DEPLOY_INFRA_SERVICE_EXISTS

Requires services infrastructure events to be published on infra.yandex-team.ru

## Rationale
There are many use-cases for the deployment data of a service. For example, after an incident, a maintainer of the affected service can check all the deployment schedules of the service dependencies and determine if the incident was caused by them.

## Solution
1. Go to the your deploy project.
1. Select production stage.
1. Go to "Config" tab.
1. Tap "Edit" button.
1. Choose service and environment for infra notifications for your deploy unit.
1. Commit changes in your repository. Example patch:
```yml
labels:
  infra_service: INFRA_SERVICE_ID
  infra_environment: INFRA_ENVIRONMENT_ID
```

{% note info %}

INFRA_SERVICE_ID - 336 (for all)

INFRA_ENVIRONMENT_ID:
* Maps - 529
* NMaps - 531
* JS API & Services - 530
* Metro - 537
* HTTP API - 538
* Backoffice admin - 539
* Others - 532

{% endnote %}

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/infra-events.test.ts#L42-46)_
