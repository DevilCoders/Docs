# API TESTS TEMPLATE

При создании нового репозитория указать этот репозиторий в качестве темплейта.

После создания репозитория:
1. Меняем в файле `api-client/pom.xml` в блоке properties тег `<oas.url>https://petstore.swagger.io/v2/swagger.json</oas.url>` на свой хост сваггера

Например:
   
    <properties>
        <oas.filename>swagger.json</oas.filename>
        <oas.directory>${project.build.directory}</oas.directory>
        <oas.url>http://autoru-cabinet-api-01-sas.test.vertis.yandex.net:2030/api-docs/swagger.json</oas.url>
        <oas.input>${oas.directory}/${oas.filename}</oas.input>
    </properties>
    
2. Выполняем: `mvn clean compile`
3. В файле `api-client/src/main/java/ru/auto/tests/example/config/ExampleApiConfig.java` меняем урлы и версию api

    ```
    @Key("example.api.testing.uri")
    @DefaultValue("http://petstore.swagger.io:80") - урл тестовой версии
    URI getExampleApiTestingURI();

    @Key("example.api.release.uri")
    @DefaultValue("http://petstore.swagger.io:80") - урл стабильной версии
    URI getExampleApiProdURI();

    @Key("example.api.version")
    @DefaultValue("v2") - верисия апи
    String getExampleApiVersion();
    ```
Например:

    @Key("example.api.testing.uri")
    @DefaultValue("http://autoru-cabinet-api-01-sas.test.vertis.yandex.net:2030/api")
    URI getExampleApiTestingURI();

    @Key("example.api.release.uri")
    @DefaultValue("http://autoru-cabinet-api-01-sas.test.vertis.yandex.net:2030/api")
    URI getExampleApiProdURI();

    @Key("example.api.version")
    @DefaultValue("1.x")
    String getExampleApiVersion();
4. Меняем наименования директорий с `example` на свои для удобства репозитория. Например на `cabinet`
5. Выполняем: `mvn clean compile` для перегенерации данных
6. В сгенеренном репозитории создается 3 теста для примера - для компиляции проекта их надо заигнорить (или написать свои нормальные)
