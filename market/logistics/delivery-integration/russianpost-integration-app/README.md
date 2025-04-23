#Интеграционное приложения для работы с Почтой России

Для локального запуска:
1. Желательна установка плагинов:
    - [.EVN](https://github.com/adelf/idea-php-dotenv-plugin)
    - [Lombok](https://github.com/mplushnikov/lombok-intellij-plugin)
2. `cd dependency-stubs` и `docker-compose up -d` запустить локально постгрес.
3. Создать конфигурацию Spring Boot с main-классом `ru.yandex.market.delivery.rupostintegrationapp.IntegrationApplication` и настройками окружения `PROPERTIES_DIR=<полный-путь-от-корня-ФС-к-аркадии>/arcadia/market/logistics/delivery-integration/russianpost-integration-app/src/main/properties.d/local;ENVIRONMENT=local`
4. для просмотра тестовой базы, можно скачать PSequel и сходить по реквизитам
    - host: `pgaas-test.mail.yandex.net:12000`
    - username and pass and database из файла `application-testing.properties`
