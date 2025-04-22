# DEPLOY_DISRUPTION_BUDGET

Requires the disruption budget of a deploy unit to be less or equal to 33% of the instance count.

## Rationale
The disruption budget determines how many instances can be unavailable (restarting) during the deployment process.  If the disruption budget is more than a third of the total instance count, a spike in traffic or a incident occurring during the deployment ca seriously affect the service SLA.

## Solution
1. Go to your deploy configuration in repository.
1. Set the `max_unavailable` value to be less or equal to 0.3 of the total replica count:
```yml
spec:
    deploy_units:
        app:
            multi_cluster_replica_set:
                replica_set:
                    clusters:
                        - cluster: man
                          spec:
                              replica_count: 1
                        - cluster: sas
                          spec:
                              replica_count: 1
                        - cluster: vla
                          spec:
                              replica_count: 1
                    deployment_strategy:
                        max_unavailable: 1
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L215-226)_
