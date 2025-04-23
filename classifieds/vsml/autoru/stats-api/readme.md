# Stats-api
Считает статистики в разрезах регион + марка/модель/суперген/конфигурация/техпарам. Замена `auto2-price-estimator`

## Run local
```bash
yav-deploy --configs-path . --deploy-root . --file yav.conf
set -o allexport; source local_config_env.lst; set +o allexport
./start.sh
```


## Run docker
```bash
yav-deploy --configs-path . --deploy-root . --file yav.conf
docker run --rm -t -i \
    --env-file local_config_env.lst \
    --network host registry.yandex.net/vertis/autoru-stats:latest
```
