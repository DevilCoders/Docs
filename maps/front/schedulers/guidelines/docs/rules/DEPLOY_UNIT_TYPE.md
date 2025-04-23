# DEPLOY_UNIT_TYPE

Requires multi-cluster replica set (MCRS) for deploy unit.

## Rationale
A multi-cluster replica set defines a "virtual" data center which can be distributed among different physical data centers. The virtual DC can have it's own configuration for the number of maximum unavailable instances.
The other kind of replica set, called Single Replica Set (SRS) requires multiple instances in each data center, and also requires a separate configuration for the maximum unavailable instances for each data center.
Most of our services are small and run on 1 instance in 3 data centers. That's why it is required for the majority of services to use MCRS for their deploy unit configuration. If you think your service should be excluded from this group contact a member of the maps-front-infra DevOps team.

## Solution
1. Go to your deploy configuration in the code repository.
1. Check that your configuration corresponds to the following scheme:
```yml
spec:
    deploy_units:
        app:
            multi_cluster_replica_set:
                replica_set:
                    ...
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L176-183)_
