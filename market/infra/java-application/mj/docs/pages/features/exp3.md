# Модуль Эксперименты 3.0

Модулем подключается клиент, который нужен для похода в [сайдкар](https://wiki.yandex-team.ru/market/development/developer-experience/adminka-konfigov/kak-podkljuchit-sajjdkar-jeksperimentov3.0) и получения оттуда конфигов.

## Установка

Добавить в `service.yaml` модуль `experiments3`:
```yaml
modules:
  experiments3:
    ...
```

## Настройка
```yaml
modules:
  experiments3:
    port: 11922
    consumer: marketplanner
    testConfigsPath: /market/infra/market-planner/exp3_configs/test_response.json
    configSchemas:
      - market/infra/market-planner/exp3_configs/test_marketplanner_root_deps_list_ids
```
***port*** - порт, на котором развернут [сайдкар](https://wiki.yandex-team.ru/market/development/developer-experience/adminka-konfigov/kak-podkljuchit-sajjdkar-jeksperimentov3.0). По умолчанию 11920.\
***consumer*** - глобальный консьюмер. Если не указан, то нужно передавать консьюмера в каждом вызове методов клиента.\
***testConfigsPath*** - путь до тестовых данных.\
***configSchemas*** - список путей, по которым находятся прото-файлы, описывающие схемы конфигов ([пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/market-planner/exp3_configs/test_marketplanner_root_deps_list_ids)). Из них после сборки сгенерируются Java-классы.
## Использование
1. Заинжектить клиента в код
```java
@Autowired
private Experiments3Client experiments3Client;
```
2. Получить конфиг или эксперимент

Ознакомиться с API сайдкара можно [здесь](https://wiki.yandex-team.ru/taxi/backend/architecture/experiments3/http/#primeryispolzovanija). Для похода в ручки API вызываем соответствующие методы клиента.

Пример получения конфига, на основании которого можно будет понять, разрешено ли какое-то действие:
```java
public boolean canDoSomething() {
    final SomeConfig.Settings config;
    try {
        // Запрашиваем конфиг: достаточно передать сгенерированный класс, к которому нужно смапить конфиг.
        // В таком случае будет использоваться консьюмер, заданный при создании клиента, а имя конфига будет браться из имени файла схемы.
        config = experiments3Client.getConfig(SomeConfig.Settings.class);
    } catch (Exp3MatcherCallException | InvalidProtocolBufferException | JsonProcessingException e) {
        log.error("Failed to get config: {}", SomeConfig.exp3ConfigName, e);
        return true;
    }
    // Работаем с полями конфига, реализуем бизнес-логику, возвращаем результат
    return !config.isForbidden();
}
```