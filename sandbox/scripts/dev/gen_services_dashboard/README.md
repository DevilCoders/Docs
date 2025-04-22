The script generates a JSON model for [Sandbox Services](https://grafana.yandex-team.ru/d/000020611/sandbox-services) dashboard.

1. Get a list of recently active services from [Clickhouse](https://wiki.yandex-team.ru/sandbox/clickhouse/#tabix):

```sql
SELECT DISTINCT service
FROM (
    SELECT service
    FROM servicestatisticsd
    WHERE date >= subtractDays(today(), 15)
    ORDER BY timestamp
)
WHERE service NOT LIKE 'statistics_processor%'
ORDER BY service;
```

2. Update `services.json`

3. Run the script

```bash
$ ya make scripts/dev/gen_services_dashboard
$ scripts/dev/gen_services_dashboard/gen_services_dashboard | ya paste
```

4. Paste the resulting JSON into Settings -> JSON Model.
