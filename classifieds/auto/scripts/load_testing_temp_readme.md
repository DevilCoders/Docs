# Заметки по запуску нагрузочных тестов.

### Пока всё в ручном режиме.

Запуск тестов происходит в 3 этапа:

1. Собрать новый образ (в админке TeamCity https://t.vertis.yandex-team.ru/project.html?projectId=Auto20)
   либо найти подходящий, список доступных образов можно взять через приватный registry:
```
curl --location --request GET 'https://registry.yandex.net/v2/vertis/auto2-searcher/tags/list' \
   --header 'Authorization: OAuth YOUR_AUTH'
```
2. Зайти на общую виртуалку auto2-searcher-01-dev.sas.yp-c.yandex.net и запустить контейнер (см. список команд). Для запуска используем порт 80 или 34389.

3. Зайти в лунапарк https://lunapark.yandex-team.ru/ и произвести стрельбы.
Запуск производить с cloud-танков (RTC), которые находятся в sas.
В качестве мишени указать: auto2-searcher-01-dev.sas.yp-c.yandex.net:80 (34389)

пример простой стрельбы - https://lunapark.yandex-team.ru/3040434

## Список полезных команд

### Список всех images
sudo docker images --all

### Список всех контейнеров
sudo docker ps --all

### Запустить контейнер
sudo docker start XXXXXXXXXXXX

### Остановить контейнер
sudo docker stop XXXXXXXXXXXX

### Удалить конкретный image
sudo docker rmi XXXXXXXXXXXX

### Удалить конкретный контейнер
sudo docker rm XXXXXXXXXXXX

### Удалить все остановленные контейнеры
sudo docker rm $(sudo docker ps --filter status=exited -q)

### Скачать image и стартовать на его основе контейнер
sudo docker run --network=host \
-e _DEPLOY_APP_VERSION='22.07.01-09.59.37-arcadia-trunk-90ba47f809' \
-e SEARCHER_HTTP_PORT=34389 \
-e _DEPLOY_HPROF_DIRECTORY='/var/run/auto2/ru/heap' \
-e ENVIRONMENT=testing \
-e AUTORU_DESKTOP_HOST='test.avto.ru' \
-e AUTORU_MEDIA_HOST='mag.test.avto.ru' \
-e AUTORU_MOBILE_HOST='m.test.avto.ru' \
-e AUTO_BROKER_URL='broker-api-lb-http.query.consul:80' \
-e AUTO_HOST='https://test.avto.ru' \
-e AUTO_MOBILE_HOST='https://m.test.avto.ru' \
-e AUTO_S3EDR_URL='http://s3.mds.yandex.net' \
-e AUTO_S3EDR_BUCKET='auto' \
-e AUTO_S3EDR_KEY='5ug8NgsTbp3fXBhruhh3' \
-e AUTO_S3EDR_KEYPREFIX='autoru-extdata' \
-e AUTO_S3EDR_SECRET='b+Ax1LOOwB14/ll7KuYgExMPkxGOuZHZzRFTfMI1' \
-e AUTO_ZK_CONN_STRING='zookeeper-legacy-01-vla.test.vertis.yandex.net:2181,zookeeper-legacy-01-sas.test.vertis.yandex.net:2181,zookeeper-legacy-01-myt.test.vertis.yandex.net:2181' \
-e SEARCHER_IDLE_TIMEOUT=60000 \
-e SEARCHER_IDLE_TIMEOUT_LOW_RESOURCES=60000 \
-e SEARCHER_MIN_OFFERS_CARS=1000 \
-e SEARCHER_MIN_OFFERS_MOTO=100 \
-e SEARCHER_MIN_OFFERS_TRUCKS=100 \
-e SEARCHER_SO_LINGER_TIMEOUT=60000 \
-e SUBS_HTTP_PORT=82 \
-e _DEPLOY_G_SENTRY_DSN='https://26f3adcf8bf6468e92f299a48bb3fcbd@sentry.vertis.yandex.net/7878' \
-e _DEPLOY_G_TVM_ID=2027612 \
-e _DEPLOY_G_TVM_SECRET='' registry.yandex.net/vertis/auto2-searcher:22.07.01-09.59.37-arcadia-trunk-90ba47f809
