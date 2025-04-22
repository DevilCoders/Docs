```
SELECT
    timestamp,
    _logfeller_timestamp,
    _timestamp,
    _partition,
    _offset,
    _idx,
    iso_eventtime,
    queueId,
    application,
    environment,
    instance,
    protocol,
    method,
    request,
    status,
    'ip123' as ip,
    user_agent,
    response_size,
    duration,
    thread,
    requestId,
    _rest,
    component,
    'x_forwarded_for_123' as x_forwarded_for,
    datacenter
FROM ott_backend_logs._ott_logs_access_log_d
WHERE
    ceil(timestamp / 1000.0) between 1658146486 and 1658146686
  AND environment = 'production'
  AND multiSearchAny(requestId
    , (SELECT groupUniqArray(requestId) from ott_backend_logs._ott_logs_access_log_d
       WHERE
         ceil(timestamp / 1000.0) between 1658146486 and 1658146686
         AND environment = 'production'
         AND match(request, 'vsid=4cdd69876fb0262e87f15b613195c84e081af6cb134bxWEBx9392x1658146586')))
```