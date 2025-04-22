# Export analytics from courier DB to analytics DB

[[toc]]

## Description

This tool is scheduled to ran in sandbox every day (see links in the bottom).
It exports 2 weeks of routes and nodes data by default, but can be configured to export any range of dates:
```
$ ./export_analytics --help
usage: export_analytics [-h] [--from-date FROM_DATE] [--to-date TO_DATE]

optional arguments:
  -h, --help            show this help message and exit
  --from-date FROM_DATE
                        Filter routes from this date, default is 2 weeks before today
  --to-date TO_DATE     Filter routes to this date, default is today
```

## Environment variables

Database shall be configured with env variables, you can use following commands to export data in corresponding environments:

```
# testing:
$ env YA_COURIER_DB_USER=$(ya vault get version sec-01ddnqwesjbm5yjadwh1fpky75 -o db_user) YA_COURIER_DB_PASSWORD=$(ya vault get version sec-01ddnqwesjbm5yjadwh1fpky75 -o password) YA_COURIER_DB_HOST=$(ya vault get version sec-01ddnqwesjbm5yjadwh1fpky75 -o hosts) YA_COURIER_DB_PORT=6432 YA_COURIER_DB_NAME=b2bgeo_courier_test ANALYTICS_DB_USER=$(ya vault get version sec-01fk5wxk8pae411x7c3x3hg9gr -o db_user) ANALYTICS_DB_PASSWORD=$(ya vault get version sec-01fk5wxk8pae411x7c3x3hg9gr -o password) ANALYTICS_DB_HOST=$(ya vault get version sec-01fk5wxk8pae411x7c3x3hg9gr -o hosts) ANALYTICS_DB_PORT=6432 ANALYTICS_DB_NAME=b2bgeo_courier_analytics_test ./export_analytics

# prod:
env YA_COURIER_DB_USER=$(ya vault get version sec-01ddr3wjvshqapcjd6fj8czpp2 -o db_user) YA_COURIER_DB_PASSWORD=$(ya vault get version sec-01ddr3wjvshqapcjd6fj8czpp2 -o password) YA_COURIER_DB_HOST=$(ya vault get version sec-01ddr3wjvshqapcjd6fj8czpp2 -o hosts) YA_COURIER_DB_PORT=6432 YA_COURIER_DB_NAME=b2bgeo_yacourier_prod ANALYTICS_DB_USER=$(ya vault get version sec-01fjyrdkdz27fc1s690hhn5dz7 -o db_user) ANALYTICS_DB_PASSWORD=$(ya vault get version sec-01fjyrdkdz27fc1s690hhn5dz7 -o password) ANALYTICS_DB_HOST=$(ya vault get version sec-01fjyrdkdz27fc1s690hhn5dz7 -o hosts) ANALYTICS_DB_PORT=6432 ANALYTICS_DB_NAME=b2bgeo_courier_analytics_prod ./export_analytics
```

## Useful links

* [Testing database](https://yc.yandex-team.ru/folders/fooooj7at8f8673omia9/managed-postgresql/cluster/mdb3411l8rning1k2loj) and [it's secret](https://yav.yandex-team.ru/secret/sec-01fk5wxk8pae411x7c3x3hg9gr)
* [Production database](https://yc.yandex-team.ru/folders/fooooj7at8f8673omia9/managed-postgresql/cluster/mdbm76bs3nsnf7j4qjf8) and [it's secret](https://yav.yandex-team.ru/secret/sec-01fjyrdkdz27fc1s690hhn5dz7)
* [Service that uses tool aggregated data](https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/ya_courier/analytics_backend/README.md)
