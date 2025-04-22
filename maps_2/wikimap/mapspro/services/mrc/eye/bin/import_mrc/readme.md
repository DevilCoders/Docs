# eye-import-mrc

## Overview
Service is responsible for import mrc images into frames format. It processes features by ```txn_id``` in historical order by small batches. New features are imported and corresponding fields are updated for the old ones. In case of unpublication or deletion flag ```deleted``` is raised. Device is created for every unique source (type and camera model are stored in ```attrs```).

It is also possible to run in manual mode with explicit specified feature ids. Only one instance can work  at time in loop mode (used pg_advisory lock).

```
eye-import-mrc \
    --syslog-tag=eye-import-mrc \
    --loop \                # run as service (load by txn_id)
    --batch=1000 \          # upload features at time
    --timeout 5 \           # wait 5 min if no new features
    --commit \              # commit import result

eye-import-mrc \            # manual mode (no commit)
    --feature-ids=ids.txt \ # explicitly specified feature ids
    --batch=1000 \          # upload features at time
    --lock-free \           # ignore pg_lock (may be dangerous)
```

## Monitoring
* [eye-mrc-import-alive](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Deye-mrc-import-alive)
* [eye-mrc-import-queue](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Deye-mrc-import-queue)
