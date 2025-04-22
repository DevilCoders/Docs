# DEPLOY_DISK_BANDWIDTH

Requires disk bandwidth guarantee greater than 15Mb.

## Rationale
It's a deploy platform's recommendation. See ((https://clubs.at.yandex-team.ru/infra-cloud/1099 post in infra-cloud club)).

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
                                  storage_class: hdd
                                  quota_policy:
                                      bandwidth_guarantee: 15728640
                                      bandwidth_limit: 31457280
```
{% note info %}

Disk bandwidth limit of deploy unit is calculated as follows:
- for SSD storage class: `bandwidth_limit = bandwidth_guarantee`
- for HDD storage class: `bandwidth_limit = 2 * bandwidth_guarantee`

{% endnote %}

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/deploy/deploy-unit.test.ts#L327-349)_
