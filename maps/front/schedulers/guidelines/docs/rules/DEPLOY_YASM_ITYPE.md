# DEPLOY_YASM_ITYPE

Requires monitorings itype of deploy equals to `maps-front`.

## Rationale
Our own itype makes it possible to use our own Golovan quota.

## Solution
1. Go to your deploy configuration in repository.
1. Check that your configuration corresponds to the following scheme:
```yml
spec:
    deploy_units:
        app:
            multi_cluster_replica_set:
                replica_set:
                    pod_template_spec:
                        spec:
                            host_infra:
                                  monitoring:
                                      labels:
                                          itype: maps-front
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L375-385)_
