# DEPLOY_DISK_SIZE

Requires minimum disk size greater than 15Gb.

## Rationale
After several incidents involving multi-gigabyte log files we're requiring to have at least 15Gb on each instance.

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
                            disk_volume_requests:
                                - id: 'DISK_NAME'
                                  quota_policy:
                                      # 15 Gb
                                      capacity: 16106127360
```

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L281-291)_
