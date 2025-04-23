# DEPLOY_UNIT_NAME

Requires prefix `app` for every deploy unit.

## Rationale
This rule is required for unification reasons to make all deploy unit names consistent.

## Solution
1. Go to your deploy configuration in repository.
1. Change the deploy unit names so that it can match the pattern `app(-\d)?`:
```yml
spec:
    deploy_units:
        app:
            ...
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L31-39)_
