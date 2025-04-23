## Price prediction API

### Deployment

- Build Docker container
- Bump version and push to registry
- Deploy with Jenkins

### Local debug

requirements:
- sample from `statistics_v2.json` (10 lines, for example)
- local version of `vertis-datasources` in directory `local-vertis-datasources`
- data files from `start.sh`

vertis-datasources template:
```
{
    "prediction-api.s3.endpoint": "http://s3.mds.yandex.net",
    "prediction-api.s3.bucket": "misc",
    "prediction-api.s3.aws_access_key_id": "<aws_access_key_id>",
    "prediction-api.s3.aws_access_secret_key": "<aws_access_secret_key>",
    "prediction-api.catalog-api.host": "autoru-catalog-api-int.vrts-slb.test.vertis.yandex.net"
}
```

run (sync):
```
python3 run.py
```

### Local run

requirements:
- local version of `vertis-datasources` in directory `/etc/yandex/vertis-datasources/` (already exists in virtual server)
- data files from `start.sh`

run (sync):
```
gunicorn "prediction_api:create_app()" -b "[::]:5000" --timeout 480
```

run (async):
```
gunicorn "prediction_api:create_app()" -b "[::]:5000"  --timeout 480 --worker-class eventlet
```

### Local Docker run

build:
```
docker build -t prediction_api_local .
```

run:
```
docker run --rm -t -i \
    -p 8895:8895 \
    -p 8896:8896 \
    -e API_PORT=8895 -e OPS_PORT=8896 \
    --volume=<path_to_vertis_datasources>:/etc/yandex/vertis-datasources/ \
    prediction_api_local
```

push:
```
docker tag prediction_api_local registry.yandex.net/vertis/prediction-api:<new_tag>
docker push registry.yandex.net/vertis/prediction-api:<new_tag>
```
