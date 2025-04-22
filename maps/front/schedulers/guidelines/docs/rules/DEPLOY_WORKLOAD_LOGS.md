# DEPLOY_WORKLOAD_LOGS

Requires transmitting logs.

## Rationale
All our services should send all logs to YT.

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
                                          transmit_logs: true
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L638-648)_
