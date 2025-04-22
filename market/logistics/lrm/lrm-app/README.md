#LRM

##Локальный запуск
1. Скопировать проперти для локального запуска<br>
`cd <your project directory>/market/logistics/lrm/lrm-app/src/main/properties.d/local`<br>
   `cp application-local.properties.dist application-local.properties`
   Параметр lrm.tvm.secret можно взять от тестовой среды
2. Установить параметры для запуска в идее:<br>
   Edit configurations...
- **Environment variables:** ``PROPERTIES_DIR=/<your project directory>/market/logistics/lrm/lrm-app/src/main/properties.d`` 
  и `ENVIRONMENT=local`
3. Поднять нужные зависимости:<br>
   * `cd <your project directory>/market/logistics/lrm/lrm-app/dependency-stubs`<br>
   * `docker-compose up -d`
4. Запустить приложение стартом в классе Lrm

##Проверка, что приложение запустилось
Открыть в браузере http://localhost:8084/ping
