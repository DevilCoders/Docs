# DEPLOY_WORKLOAD_READINESS

Requires readiness check to be set for each workload.

## Rationale
The readiness of an instance can be defined as "the service is up and ready to accept traffic". Usually that means that the application inside the container responds to HTTP GET `/ping` requests. This check is used by Yandex.Deploy during deploy time.
Note that the same endpoint is used as our `http-ping` monitoring, which tries to determine the status of application instance.

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
                                            readiness_check:
                                                 http_get:
                                                     expected_answer: ""
                                                     path: "/ping"
                                                     port: 80
                                                     time_limit:
                                                         max_execution_time_ms: 1000
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L536-547)_
