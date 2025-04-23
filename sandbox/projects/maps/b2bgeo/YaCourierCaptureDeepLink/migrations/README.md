ClickHouse cluster: `clickhouse.metrika.yandex.net`
Database: `maps_b2bgeo`

In table `tracked_couriers` we store currently tracked couriers.
Couriers are removed from the table when we don't need to track them anymore.
DB migrations are applied manually.
