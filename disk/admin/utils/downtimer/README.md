# Install
```
[[ -d "$ARCADIA_PATH" ]]        || { echo -e "ERR: You must set env_var:\n  echo 'export ARCADIA_PATH=\"\$HOME/arcadia\"' >> ~/.bashrc"; exit 1; }
[[ -n "$JUGGLER_OAUTH_TOKEN" ]] || { echo -e "ERR: You must set env_var:\n  echo 'export JUGGLER_OAUTH_TOKEN=\$(cat \$HOME/.juggler_token)' >> ~/.bashrc"; exit 1; }

ya make --checkout -j0 "$ARCADIA_PATH/disk/admin/utils/downtimer"
```

# Run

## Run test
```
ya make --checkout -j0 "$ARCADIA_PATH/disk/admin/utils/downtimer"
./downtimer -t sas 22:00
./downtimer --test vla 22:00
```

## Run prod
```
ya make --checkout -j0 "$ARCADIA_PATH/disk/admin/utils/downtimer"
./downtimer sas 22:00
```


# Config example
```
### dt.yaml

some_name:
  namespace:
    - namespace_one
    - namespace_two
  host:
    - '%conductor_group@dc'
    - some_host
  service:
    - UNREACHABLE
    - some_service

other_name:
  namespace: some_common_namespace
  groups:
    - host:
        - host_one
        - host_two
      service:
        - some_service
    - host:
        - host_three
        - host_four
      service: another_service
```

# Downtimes generated example
```
{'namespace': 'disk', 'host': 'disk_api', 'service': 'mpfs-intapi'}
{'namespace': 'disk', 'host': 'disk_api', 'service': 'mpfs-api'}
{'namespace': 'disk', 'host': 'CGROUP%disk_mpfs@sas', 'service': 'log-reader'}
{'namespace': 'disk', 'host': 'CGROUP%disk_docdb@sas', 'service': 'mongodb-replica-lag'}
{'namespace': 'disk', 'host': 'CGROUP%disk_uploader@sas', 'service': 'uploader'}
<...>
{'namespace': 'telemost', 'host': 'telemost.stage.telemost_mediator-balancer_stable', 'service': 'upstream-dc'}
{'namespace': 'telemost', 'host': 'telemost.stage.telemost_mediator_stable', 'service': 'upstream-dc'}

Downtime until: 2022-03-23 21:00:00
```
