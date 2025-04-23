## Build
1. Download data and models using in service
```bash
./deploy/load_data.sh
```
2. Compile protobuf
```bash
./deploy/protogen.sh
```

## Deploy
1. Create docker image and push into registry
```bash
./deploy/deploy.sh 'YOUR MESSAGE' VERSION
```
2. Deploy in testing
  - 1) Go to https://admin.vertis.yandex-team.ru/services/realty-price-predictor/
  - 2) Build with Parameters
```
APP_VERSION: VERSION
Message: YOUR MESSAGE
```

#### Launch in docker on local machine (Linux only)

1. Build docker image:
docker build -t price_predictor_VERSION .
2. Run docker image to test:
docker run --rm -t -i -p 8895:8895 price_predictor_VERSION

!if you need to start prod container locally:
docker run --rm -t -i -p 8895:8895 --env YDB_ENDPOINT=ydb-ru.yandex.net:2135 --env YDB_DATABASE=/ru/verticals/production/realty --env YDB_TOKEN={some_ydb_token} --env MSD_S3_URL=http://s3.mds.yandex.net --env MSD_S3_BUCKET=realty --env MSD_S3_KEY_ID={some_mds_s3_key_id} --env MSD_S3_KEY_SECRET={some_mds_s3_key_secret} --env API_PORT=8895 --env _DEPLOY_METRICS_PORT=8896 price_predictor_VERSION

3. to check healthness and testing:
python3 ./stress-test/create_request_offer.py


