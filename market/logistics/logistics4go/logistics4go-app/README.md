# Logistics4Go

## Локальный запуск

1. Скопировать проперти для локального запуска<br>
   * `cd src/main/properties.d/local`<br>
   * `cp application-local.properties.dist application-local.properties`


2. Установить параметры для запуска в идее:<br>
**Environment variables:**<br>
   * `PROPERTIES_DIR=/<path to arcadia>/market/logistics/logistics4go/logistics4go-app/src/main/properties.d;`<br>
   * `ENVIRONMENT=local`


3. Поднять нужные зависимости:<br>
    * `cd dependency-stubs`<br>
    * `docker-compose up -d`


4. Запустить приложение стартом в классе Logistics4Go
