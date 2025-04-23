# DEPLOY_ONLY_ABC_ACCESS

Prohibits personal accesses.

## Rationale
Personal access to internal services is considered harmful.  If a crucial access right is assigned only to a person it will be rendered read-only when that person takes their annual leave or gets sick. That's why only access through ABC roles are allowed.

## Solution
1. Go to your deploy project.
1. Tap "Manage Roles" link in "General access" section.
1. You will be moved to IDM.
1. Remove all personal access from the presented list.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/access.test.ts#L30-38)_
