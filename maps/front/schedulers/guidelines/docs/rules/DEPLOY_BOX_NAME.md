# DEPLOY_BOX_NAME

Require postfix `_box` for every box.

## Rationale
This rule is required for unification reasons to make all box names consistent.

## Solution
1. Go to your deploy configuration in repository.
1. Change the box names so that it can match the pattern `.*_box`:
- for multi cluster replica set
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
                                    boxes:
                                        - id: app_box
                                        ...
                                     workloads:
                                         - id: app_workload
                                           box_ref: app_box
                                         ...
```
- for replica set
```yml
spec:
    deploy_units:
        app:
            replica_set:
                replica_set_template:
                    pod_template_spec:
                        spec:
                            boxes:
                                - id: app_box
                                ...
                             workloads:
                                 - id: app_workload
                                   box_ref: app_box
                                 ...
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L88-99)_
