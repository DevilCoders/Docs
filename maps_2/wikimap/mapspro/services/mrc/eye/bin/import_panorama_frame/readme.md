# eye-import-panorama-frame

## Overview
Service is responsible for importing cut outs from panoramas into Eye frames. It processes panoramas orderd by tuple ```<txn_id, session_id, order_num>``` in historical order by batches. In a case a panorama is marked as deleted its frames are marked deleted as well. Device is created for every panorama session and frame deviations so that frames with same deviation from same session can be sequenced together. Camera model is the same for all panorama frames. It is a perfect undistorted projection to a plane.

Only one instance can work at time. For synchronisation pg_advisory lock is used.

```
=eye-import-panorama-frame \
    --syslog-tag=eye-import-panorama-frame \
    --loop \                # run as service (load by txn_id)
    --batch=1000 \          # load panoramas at time
    --timeout 5 \           # wait 5 min if no new panoramas
    --commit \              # commit import result

```

## Monitoring
* [eye-panorama-frame-import-alive](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Deye-panorama-frame-import-alive)
* [eye-panorama-frame-import-queue](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Deye-panorama-frame-import-queue)
