## Как написать новую ручку с помощью MJ?

### 1. Добавить новый path в ключ paths в src/main/resources/openapi/api/api.yaml

Документация по api.yaml: https://wiki.yandex-team.ru/market/development/developer-experience/mj-framework/api.yaml/

Документация OpenApi: https://swagger.io/specification/

### 2.Сделать  Build -> Regenerate and Reload

Если не срабатывает генерация, помогает потрогать файл MJGenerator:

```bash
touch ${ARCADIA_ROOT}/market/infra/java-application/mj/v1/src/main/java/ru/yandex/market/framework/generator/MarketJavaGenerator.java
```

### 3. Реализовать новый метод в DefaultApiDelegateImpl

### 4. Написать тесты с использованием BasePlannerWebTest

### 5. Готово
