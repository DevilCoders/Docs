# DEPLOY_TVM

Requires TVM deploy unit.

## Rationale
All services should interact with each other only using [TVM](https://wiki.yandex-team.ru/passport/tvm2) as authorization mechanism.

## Solution
1. Go to your deploy configuration in repository.
1. Check that your configuration corresponds to the following scheme:
```yml
spec:
    deploy_units:
        app:
            tvm_config:
                mode: "enabled"
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L246-254)_
