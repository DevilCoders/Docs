#### How to build
```
ya package --docker package.json
```
#### How to release:
```
ya package --docker  --docker-push  package.json
```
After that update service in QLOUD(with 'latest' tag).
#### How to run locally:
```
docker run \
    -e PAYSYS_PG_DB_HOST=x,y,z \
    -e PAYSYS_PG_DB_PORT=6123 \
    -e PAYSYS_PG_DB_NAME=x \
    -e PAYSYS_PG_DB_USER=x \
    -e PAYSYS_PG_DB_PASS=x \
    -e QLOUD_ENVIRONMENT=local \
    -it registry.yandex.net/scrooge/v1:latest
```
Build log is in the file `zless scrooge.latest.tar.gz`
`QLOUD_ENVIRONMENT=local` needed to skip configuration of push-client
`PAYSYS_PG_*` variables needed to configure /root/.pgpass to simplify database connection
