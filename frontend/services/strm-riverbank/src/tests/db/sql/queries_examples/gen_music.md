```
SELECT
    date,
    vsid,
    ottsession,
    min_timestamp,
    max_timestamp
FROM riverbank_session_aggregates
WHERE
    date = toDate('2022-07-28') AND
    vsid = 'ril1y2ztrf3p3a5l9fqa4ox5kz1h77dz64qk53x2mqp3xMIOx0582x1658992146'
```