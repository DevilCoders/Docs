```
SELECT
    iso_eventtime,
    timestamp,
    date,
    vsid,
    uuid,
    method,
    request_uri,
    'login' as yandex_login,
    'login' as webauth_login,
    12334567 as yandexuid,
    body_size,
    status,
    bytes_sent,
    request_time,
    error,
    isFatal,
    'xffy' as xffy,
    'cookie' as cookie,
    _rest,
    _logfeller_timestamp,
    _timestamp,
    _partition,
    _offset,
    _idx
FROM drm_proxy_logs.video_rt_vh_internal_drm_proxy
WHERE
    toDate(_timestamp) == toDate('2022-07-07')
  AND vsid == 'vsid'
```