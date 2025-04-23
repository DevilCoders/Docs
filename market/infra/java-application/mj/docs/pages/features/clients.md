# Генерация клиентов
MJ позволяет генерировать клиентов по OpenApi спецификации. Генерация происходит во время сборки, а использование клиентов происходит через `@Autowired`.

## Создание клиента к MJ сервису
Достаточно указать только путь до OpenApi спецификации. Все остальные параметры вычислятся из `service.yaml` этого сервиса.
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
```
{% note warning %}

В MJ сервисе OpenApi спецификация должна лежать по стандартному пути: `src/main/resources/openapi/api/api.yaml`. Иначе вместо пути до спецификации надо указать путь до `service.yaml`:
```yaml
list:
  mj-service:
    service_yaml_path: market/dev-exp/services/mj-service/service.yaml
```

{% endnote %}

По умолчанию, настройки клиента берутся из целевого сервиса для того же окружения, в котором запущено ваше приложение. Например, в `prodution`-е клиент будет ходить в `production` целевого сервиса, в `testing`-е - в `testing`.
Чтобы изменить это поведение, например, для того, чтобы из вашего `testing` окружения клиент ходил в `prestable` целевого сервиса или из `local` окружения ходить в `testing`, можно использовать проперти `dstEnv`:
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    env:
      testing:
        dstEnv: prestable
      local:
        dstEnv: testing
```

## Создание клиента к любому сервису
Все значения ниже можно переопределять для разных сред, как описано [здесь](../how_it_works/configuration/environment.md).

Помимо пути до openapi спецификации, нужно обязательно задать url.
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
```

Если сервис защищен TVM, то нужно указать TVM id этого сервиса, чтобы автоматически в заголовок запроса добавлялись Service Ticket и User Ticket.
```yaml
list:
   mj-service:
      openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
      url: http://localhost:8080
      tvm:
         dstId: 3333
```

Чтобы отключить генерацию Service Ticket-ов и/или User Ticket-ов, можно указать следующие параметры:
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
    tvm:
      serviceTicketEnabled: false
      userTicketEnabled: false
```

Также есть возможность задать трассировочный модуль.
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
      url: http://localhost:8080
      trace:
        targetModule: MJ_SERVICE
```

Отключить трассировку можно так:
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
    trace:
      enabled: false
```

Если беспокоит обилие логов неудачных запросов (`status code != [200..300)`), то логирование можно отключить:
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
    logging:
      logUnsuccessful: false
```

## Динамическое изменение url в каждом запросе
Иногда бывают ситуации, когда url неизвестен на этапе конфигурирования приложения или необходимо ходить на разные хосты.
Для таких случаев для каждой ручки, помимо основного метода, который неявно использует url, заданный в service.yaml,
генерируется еще два дополнительных метода:
```java
public ExecuteCall<String, RetryStrategy> helloWorldGet(
        String baseUrl, boolean appendPath, String name
)

public ExecuteCall<String, RetryStrategy> helloWorldGet(
        String baseUrl, String name
)
```
В обоих случаях передается url, но в первом варианте можно подставить полностью кастомный url в `baseUrl`, если 
`appendPath=false`, а во втором - к `baseUrl` будет добавляться уже существующий path.
## Как воспользоваться сгенерированными клиентами
Чтобы воспользоваться сгенерированным клиентом, достаточно добавить его в код с аннотацией `@Autowired`.
Найти имя класса для клиента можно двумя способами.
1. Посмотреть в соответствующей OpenApi спецификации тег (именем класса будет `<имя тега в camelCase>ApiClient`)
2. Найти класс в папке со сгенерированным кодом
   ![](https://jing.yandex-team.ru/files/sid-hugo/image%20%286%29.png)
