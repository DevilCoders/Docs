Приложение для мока сервисов Необходим для поднятия приложения jsonapi без внешних зависимостей от сервисов

Для поднятия jsonapi с этим сервисом нужно:
1. Поднять `MockApp`, запомнить host и port, где поднято приложение
2. Поднять `jsonapi.App`:
    1. с профилем `spring.profiles.active=mock`
    2. с переменными окружения (необходимо заполнить корректно):
    ```
    DEPLOY_TVM_TOOL_URL=http://localhost:18080;
    TVMTOOL_LOCAL_AUTHTOKEN=***;
    MYSQL_HOST=dev-partner;
    MYSQL_PORT=3306;
    MYSQL_USER=;
    MYSQL_PASSWORD=;
    MOCK_SERVER_HOST=<Взять из пункта 1>;
    MOCK_SERVER_PORT=<Взять из пункта 1>
    ```
