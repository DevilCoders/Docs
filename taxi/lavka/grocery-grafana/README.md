Maintainer: Daria Vasileva darrie@yandex-team.ru

19.07.2022 registry.yandex.net/eda/grocery-grafana/20220719122837-prod-
- first working image for grocery-grafana
- ldap authorization with staff login/password
- vertamedia-clickhouse-datasource plugin installed
- supervisorctl-managed
- clickhouse&pg as datasources
- grocery_grafana pg database as grafana database
- env variables (e.g. db password) stored as Nanny env variables 
