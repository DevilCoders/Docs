# API тесты

`carfax-tests` - тесты для http://carfax-api-http.vrts-slb.test.vertis.yandex.net   
`recall-tests` - тесты для http://recalls-api-http-api.vrts-slb.test.vertis.yandex.net 

Для локальной разработки всегда перед началом:
```
$ mvn clean install -DskipTests
```
 
Библиотечки, которые мы используем:
1. [jUnit 4](https://junit.org/junit4/) - ну тут все понятно) Надо бы сподобиться и съехать на ScalaTest или Junit5 хотя бы)
2. [OpenAPI generator](https://github.com/OpenAPITools/openapi-generator) - с помощью этой штуки мы генерим RestAssured клиент
из swagger документации и модельки от туда же
3. [AssertJ](https://assertj.github.io/doc/) - более умные ассерты, которые генерятся по моделькам 

Запускаются тесты автоматически в тимсити:  
[carfax-tests](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=VerticalsBackend_Carfax_RunCrafaxIntegrationTests)
и [recall-tests](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=VerticalsBackend_Carfax_RunRecallApiIntegrationTests)  
  
Запускает их Hubot, отчеты в чатик тоже от туда прилетают:
[carfax-tests](https://github.com/YandexClassifieds/vertis-hubot/blob/master/src/flows/cafax-api-test-results.coffee)
и [recall-tests](https://github.com/YandexClassifieds/vertis-hubot/blob/master/src/flows/recall-api-test-results.coffee)  
