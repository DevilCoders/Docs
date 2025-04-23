# DEPLOY_WORKLOAD_LIVENESS

Requires that liveness check for each workload is enabled.

## Rationale
The liveness of an instance is defined as "the container started normally and basic services are ready". Usually it means that there is web server listening and responding on TCP 80.

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
                            pod_agent_payload:
                                  spec:
                                      workloads:
                                          - id: app_workload
                                            liveness_check:
                                                tcp_check:
                                                    port: 80
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L491-502)_
