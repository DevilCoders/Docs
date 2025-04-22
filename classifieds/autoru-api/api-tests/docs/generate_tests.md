## Генерация тестов

Можно генерить из swagger не только клиент, но и тесты    

Для этого надо в [public-api-client/pom.xml](../public-api-client/pom.xml)
в плагине `openapi-generator-maven-plugin` поменять значение  
```xml
<generateApiTests>false</generateApiTests>
```
и запустить `mvn clean install -DskipTests`  

Когда проект скомпилится - появится папка с тестами в 
[public-api-client/target/generated-sources/openapi-generator/src/test/java/ru/auto/tests/publicapi/api/](../public-api-client/target/generated-sources/openapi-generator/src/test/java/ru/auto/tests/publicapi/api/)  
Единственное, что остается - перенести нужные тесты из `generated-sources`  

Сложности:
1. Тесты `CatalogApiTest` и `PhotosApiTest` генерятся неправильно из-за переноса строк в swagger. Поэтому мы не можем 
оставить генерацию тестов всегда включенной :(
2. Тесты генерятся - из-за этого там закомментированно много, нет авторизации для ручек где это надо и т.д. - надо 
внимательно на них смотреть после копирования и "допиливать"  


После того, как тесты перенесли в `public-api-tests` из `generated-source` советую опять проставить `generateApiTests` в `false` и перекомпилить все  
После этого все сгенеренные тесты из `generated-source` пропадут