# DEPLOY_WORKLOAD_UNISTAT

Requires the presence of a unistat endpoint with a specific name.

## Rationale
By default Golovan uses `/unistat` as endpoint. We chose not change this value and so it is the required name for unistat.

## Solution
1) Go to your deploy configuration in repository.
2) Check that your configuration corresponds to the following scheme:
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
                                      - workload_id: app_workload
                                        port: 7032
                                        path: /unistat
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L440-462)_
