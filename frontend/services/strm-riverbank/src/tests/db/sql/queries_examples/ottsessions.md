```
SELECT
    date,
    vsid,
    ottsession,
    min_timestamp,
    max_timestamp
FROM riverbank_session_aggregates
WHERE
    date = toDate('2022-07-07') AND
    vsid = 'vsid'
```