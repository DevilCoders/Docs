# Service for sending aggregated statistics of MRC feedback tasks to Clickhouse.

### Read MRC Postgres DB (db.h/cpp)
Read map: feedback task ID -> earliest source (private/public app, panorama etc.).
Consider all data domains: addresses, signs, traffic lights.

### Read social Postgres DB (social.h/cpp)
Read social.feedback_task for IDs, including commits.

### Aggregate (counter.h/cpp)
Group tasks by sources, days, feedback types,
separately by waiting, rjected, accepted and accepted with commits.

### Write to Clickhouse (clickhouse.h/cpp)
Save result to Clickhouse.

### Dashboard
https://datalens.yandex-team.ru/t5tsie3281m0o-feedback