# DEPLOY_WORKLOAD_STOP_POLICY

Requires the stop policy of each workload set with a certain template.

## Rationale
It's used during deploy time to seamlessly switch traffic between the old and new version: the current instance will be closed, Yandex.Deploy will wait for the current requests to be processed and only then the instance will be destroyed.

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
                                          stop_policy:
                                              container:
                                                  command_line: bash -c "/detach.sh"
                                                  time_limit:
                                                      max_execution_time_ms: 20000
                                                      max_restart_period_ms: 30000
                                                      min_restart_period_ms: 30000
                                              max_tries: 2
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L580-612)_
