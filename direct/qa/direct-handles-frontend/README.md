direct-handles-frontend
=======================

Direct Handles frontend static files

### Собрать локально Docker образ
```
docker build -t direct-qa/applications:direct-handles-static-latest .
```

### Запустить локально на http://localhost:8080/
С локальным `direct-handles-rest`:
```
docker run \
  -e DIRECT_HANDLES_URL=http://localhost:9002 \
  -e BALANE_PROXY_URL=http://localhost:9002 \
  -e QLOUD_HTTP_PORT=8080 \
  -p 8080:8080 \ 
  direct-qa/applications:direct-handles-static-latest
```
Параметры тестинга (из конфига https://deploy.yandex-team.ru/stage/direct-handles-test/config):
```
  -e DIRECT_HANDLES_URL=https://direct-handles-test.qart.yandex-team.ru/direct-handles-rest \
```
Прода (https://deploy.yandex-team.ru/stage/direct-handles-prod/config):
```
  -e DIRECT_HANDLES_URL=https://direct-handles.qart.yandex-team.ru/direct-handles-rest \
```
