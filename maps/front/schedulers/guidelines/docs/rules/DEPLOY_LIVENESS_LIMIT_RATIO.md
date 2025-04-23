# DEPLOY_LIVENESS_LIMIT_RATIO

Requires liveness limit ratio equal to 1.

## Rationale
Part of instances are removed from endpoint_set during deployment process. So Juggler removes them from its own group and call an alert because of more than one third instances are unavailable. See ((https://st.yandex-team.ru/RTCSUPPORT-8660#60257e32140d331ea1ee9313 RTCSUPPORT-8660)).

## Solution
1. Go to your deploy configuration in repository.
1. Check that your configuration corresponds to the following scheme:
```yml
spec:
    deploy_units:
        endpoint_sets:
            - id: http
              liveness_limit_ratio: 1
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L405-413)_
