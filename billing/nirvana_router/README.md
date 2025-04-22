nirvana router
================

route nirvana queries to different test environments

to run 
```bash
ya make && PG_DB_PASSWORD="XXXXXX" ./nirvana_router
```

to build and upload docker container
```bash
ya package --docker --docker-push --target-platform linux  --docker-repository paysys-test package.json
```

application is hosted here: https://platform.yandex-team.ru/projects/paysys/nirvana-router/testing

curl example
```bash
curl -v https://nirvana-router-test.paysys.yandex-team.ru/v2/call/db2json/xxx1\?ticket\=22
```
