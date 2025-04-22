## realty-price-predictor

### Разработка
#### Зависимости
1. Установите Docker (можно из SelfService)
2. Все зависимости лежат в `requirements.txt`, установить можно как
```
pip install -r requirements.txt
```
#### Пакетирование
1. Сборка образа осуществляется с помощью `ya package`, а именно
```
ya package package.json --docker --docker-repository=vertis --docker-push
```
2. Локально можно запустить через `bash ./start.sh`, однако настоятельно рекомендуется запускать собранный образ.
Команда выглядит таким образом (в проде эти переменные заполняются из манифеста):
```
docker run --rm -t -i \
-p 8895:8895 \
-p 8896:8896 \
--env API_PORT=8895 \
--env _DEPLOY_METRICS_PORT=8896 \
--env YDB_ENDPOINT=ydb-ru.yandex.net:2135 \
--env YDB_DATABASE=/ru/verticals/production/realty \
--env YDB_TOKEN=<ydb_secret> \
--env MDS_S3_URL=http://s3.mds.yandex.net \
--env MDS_S3_BUCKET=realty \
--env MDS_S3_KEY_ID=<mds_key> \
--env MDS_S3_KEY_SECRET=<mds_secret>
registry.yandex.net/vertis/realty-price-predictor:yourversion
```


### Сборка и деплой
1. На каждый коммит в PR в аркадийном CI запускается сборка docker-образа c версией `1.1.launch_N`.
Все подобные сборки можно увидеть на [странице](https://a.yandex-team.ru/projects/vsinfr/ci/actions/launches?dir=classifieds%2Fvsml%2Frealty%2Fprice_estimator%2Fprice-estimator-rest-api&id=realty-price-predictor-commit-build-flow).

   Далее версию можно выкатить **руками** в [админке деплоя](https://admin.vertis.yandex-team.ru/services/realty-price-predictor).
2. После вливания PR в `trunk`, можно запустить релиз: сборку контейнера версии `1.1.revision` и выкладку этой версии в тестинг. Далее эту версию можно покатить в продакшен через PROMOTE.


#### Тестирование
#### unit
1. Install pytest
```
pip3 install pytest
```
2. Run tests
```
pytest -v test/test_model_updating.py
pytest -v test/test_protobuf.py
pytest -v test/test_stats_container.py
```

#### inference
```
quality_today_test.py [-h] [--path PATH] [--hostname HOSTNAME] [--table_path TABLE_PATH] [--data_path [DATA_PATH]] [--protobuf_model PROTOBUF_MODEL]
```

`--table_path` - table in YT with offers test set:
- //home/verticals/realty/price_estimator/monitoring/rent_apartment_test_set
- //home/verticals/realty/price_estimator/monitoring/sell_apartment_test_set

`--path` route in API (define model to predict):
- get_price_offer
- get_price_custom
- get_price_landing

`--hostname` address to service (test or local):
- realty-price-predictor-api.vrts-slb.test.vertis.yandex.net
- localhost:8895

`--protobuf_model` select protobuf model for generated requests:
- offer (default, for `OfferMessage`)
- landing (for `PricePredictionLandingRequest`)

`--data_path` filename to save results (optionally)

example:
```
python3 ./test/quality_today_test.py \
  --table_path //home/verticals/realty/price_estimator/monitoring/rent_apartment_test_set\
  --path get_price_offer\
  --hostname realty-price-predictor-api.vrts-slb.test.vertis.yandex.net
```

