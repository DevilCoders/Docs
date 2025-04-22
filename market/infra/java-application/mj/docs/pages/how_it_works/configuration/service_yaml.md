# service.yaml

**service.yaml** - является файлом, содержащим описание сервиса и его настройки. Он должен лежать в корне кода сервиса.

{% note info %}

Чтобы задавать параметры для разных окружений целевого сервиса, надо использовать [метод переопределения значений для разных окружений](environment.md).
Итоговая конфигурация может выглядеть примерно так:
```yaml
list:
  taxi_authproxy:
    openapi_spec_path: taxi/backend-py3/services/taxi-corp-integration-api/docs/yaml/api/authproxy.yaml
    env:
      local:
        url: "http://corp-integration-api.taxi.tst.yandex.net"
      production:
        url: "http://corp-integration-api.taxi.yandex.net"
      testing:
        url: "http://corp-integration-api.taxi.tst.yandex.net"
    tvm:
      env:
        local:
          dstId: 2002374
        production:
          dstId: 2002372
        testing:
          dstId: 2002374
    trace:
      targetModule: TAXI_CORP_INTEGRATION_API
```

{% endnote %}

## Обязательные поля
К обязательным полям относятся:
- java_service.service_name
- java_service.deploy_type
- trace.module

Все остальные поля являются опциональными и нужны для добавления каких-либо фич фреймворка.

## Описание полей
**Содержание**


- [java_service](#java_service):
  - [service_name](#service_name)
  - [root_package](#root_package)
  - [packages_to_scan](#packages_to_scan)
  - [deploy_type](#deploy_type)
  - [ya_ide](#ya_ide)
- [trace](#tracemodule)
  - [module](#tracemodule)
- [server](#serveropenapispecpath)
  - [openapiSpecPath](#serveropenapispecpath)
- [clients](#clients)
  - [list](#list)
    - [openapi_spec_path](#openapi_spec_path)
    - [service_yaml_path](#service_yaml_path)
    - [dstEnv](#dstenv)
    - [url](#url)
    - [tvm](#tvm)
      - [dstId](#dstid)
      - [serviceTicketEnabled](#serviceticketenabled)
      - [userTicketEnabled](#userticketenabled)
    - [trace](#trace)
      - [targetModule](#targetmodule)
      - [enabled](#enabled)
    - [fault_tolerance](#fault_tolerance)
- [tvm](#tvm-self)
  - [id](#id)
  - [sources](#sources)
  - [destinations](#destinations)
  - [serverTvmDisabled](#servertvmdisabled)
  - [clientsTvmDisabled](#clientstvmdisabled)
- [modules](#modules)
- [generation_settings](#generation_settings)
  - [ya_make_dependencies](#ya_make_dependencies)
  - [modules_templates](#modules_templates)
  - [api_service_classes](#api_service_classes)


### java_service
#### service_name
Название сервиса. Например:
```yaml
java_service:
  service_name: test_service
```

#### root_package
Корневой пакет проекта. При создании сервиса через СПОК, автоматически подставляется пакет, заданный в интерфейсе СПОКа. По умолчанию используется пакет `ru.yandex.market.<service_name>`

#### packages_to_scan
Массив строк, где можно указать пакеты, которые должен сканировать Spring. По умолчанию сканируется весь `root_package`

#### deploy_type
Здесь указывается, куда будет выкладываться сервис: в Yandex Deploy (значение `yandex_deploy`) или в Nanny (значение `nanny`). Если значение не указано, то считается, что сервис выкладывается в Yandex Deploy.
```yaml
java_service:
  deploy_type: yandex_deploy
```

#### ya_ide
Пользовательская настройка флагов для ya ide idea. Подробнее [здесь](../../features/generation_settings.md#Пользовательская-настройка-флагов-для-ya-ide-idea)

#### lang
Здесь можно указать `kotlin`, чтобы класс имплементации ручек генерировался на Kotlin. Значение по-умолчанию: `java`.

### trace.module
Модуль трассировки из файла [Modules.java](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/request/request-utils/src/main/java/ru/yandex/market/request/trace/Module.java) (должен существовать в файле). Например:
```yaml
trace:
  module: TSUM_API
```

### server.openapiSpecPath
Кастомный путь до файла OpneApi спецификации
```yaml
server:
  openapi_spec_path: market/my-service/src/main/resources/openapi/custom/path/api.yaml
```

### clients
Раздел для указания openapi спецификаций к сервисам, к которым хочется сгенерировать клиент, а так же настройки для этих клиентов.

[comment]: <> (TODO: сделать ссылку на clients.md)

Содержит 2 раздела:
* **list** - для указания путей до openapi спецификаций и того, какие пресеты настроек применить
* **fault_tolerance_presets** - для указания пресетов настроек

#### list
Список клиентов, которые необходимо создать. Для каждого клиента нужно задать id и под ним указать параметры для создания клиента.

##### openapi_spec_path
Путь до openapi спецификации. Если сервис на MJ, то все необходимые параметры вычислятся из service.yaml этого сервиса.
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
```

{% note warning %}

В этом MJ сервисе openapi спецификация должна лежать по стандартному пути: `src/main/resources/openapi/api/api.yaml`. Иначе вместо пути до спецификации надо указать путь до `service.yaml` с помощью поля [service_yaml_path](#service_yaml_path)

{% endnote %}

##### service_yaml_path
Путь до service.yaml целевого сервиса для клиента.

{% note warning %}

Может использоваться только для сервисов, написанных на MJ, если openapi спецификация лежит не по стандартному пути.

{% endnote %}

```yaml
list:
  mj-service:
    service_yaml_path: market/dev-exp/services/mj-service/service.yaml
```

##### dstEnv
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

##### url
Помимо пути до openapi спецификации, задать url.

{% note warning %}

Используется, если нужно сгенерировать клиент не для MJ сервиса. Для MJ сервисов это подхватывается автоматически.

{% endnote %}

```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
```

##### tvm
Если сервис защищен TVM, то можно указать настройки TVM этого сервиса, чтобы автоматически в заголовок запроса добавлялись Service Ticket и User Ticket.

###### dstId
Указание TVM id целевого сервиса.

{% note warning %}

Используется для генерации клиентов к не MJ сервисам. Для MJ сервисов это подхватывается автоматически.

{% endnote %}

```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
    tvm:
      dstId: 3333
```

###### serviceTicketEnabled
Отключение генерации Service Ticket-ов
```yaml
list:
  mj-service:
  openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
    tvm:
      serviceTicketEnabled: false
```

###### userTicketEnabled
Отключение генерации User Ticket-ов
```yaml
list:
  mj-service:
  openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
    tvm:
      userTicketEnabled: false
```

##### trace
Настройка трассировки

###### targetModule
Указание модуля трассировки из [Modules.java](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/request/request-utils/src/main/java/ru/yandex/market/request/trace/Module.java).

{% note warning %}

Используется для генерации клиентов к не MJ сервисам. Для MJ сервисов это подхватывается автоматически.

{% endnote %}

```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
    trace:
      targetModule: MJ_SERVICE
```

###### enabled
Включение/отключение трассировки
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
    trace:
      enabled: false
```

##### logging
Настройка логирования

###### logUnsuccessful
Включение/отключение логирования неудачных (`status code != [200..300)`) запросов. По-умолчанию `true`.
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
    logging:
      logUnsuccessful: false
```

##### fault_tolerance
В этом блоке можно указать id пресетов, заданных в соседнем разделе [fault_tolerance_presets](#fault_tolerance_presets).
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
    fault_tolerance:
      circuit_breaker_id: my_circuit_breaker_1
      retry_id: my_retry
      timeout_id: my_timeout
      rate_limiter_id: my_rate_limiter
```
Есть дефолтные пресеты с id `mj`, которые не надо описывать в разделе [fault_tolerance_presets](#fault_tolerance_presets).
```yaml
list:
  mj-service:
    openapi_spec_path: market/dev-exp/services/mj-service/src/main/resources/openapi/api/api.yaml
    url: http://localhost:8080
    fault_tolerance:
      circuit_breaker_id: mj
      retry_id: mj
      timeout_id: mj
      rate_limiter_id: mj
```
Список дефолтных значений:
- [Circuit breaker](https://resilience4j.readme.io/docs/circuitbreaker#create-and-configure-a-circuitbreaker)
- [Rate limiter](https://resilience4j.readme.io/docs/ratelimiter#create-and-configure-a-ratelimiter)
- [Retry](https://resilience4j.readme.io/docs/retry#create-and-configure-retry)
- [Timeout](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/java-application/mj/v1/yaml-properties/src/main/java/serviceyaml/clients/TimeoutProperties.java?rev=r9098885#L4)



#### fault_tolerance_presets
Раздел указания пресетов настроек для клиентов. Доступно 4 модуля:
* circuit_breakers
* retries
* rate_limiters
* timeouts

Каждый подраздел представляет из себя словарь, в котором ключ - это id пресета, а значение - объект с параметрами. Id используется в секции [clients_module.clients](#fault_tolerance_presets).

Параметры для настройки каждого модуля пресета можно найти в документации соответствующего модуля resilience4j:
- [Сircuit breaker](https://resilience4j.readme.io/docs/circuitbreaker#create-and-configure-a-circuitbreaker)
- [Rate limiter](https://resilience4j.readme.io/docs/ratelimiter#create-and-configure-a-ratelimiter)
- [Retry](https://resilience4j.readme.io/docs/retry#create-and-configure-retry)
- timeout:
  * connect_timeout_millis
  * request_timeout_millis
  * read_timeout_millis


В service.yaml параметр нужно записывать не в camelCase, а в snake_case (напр. вместо `failureRateThreshold` в service.yaml надо писать `failure_rate_threshold`).

{% note warning %}

На текущий момент доступны только параметры типа number, boolean, enum. То есть пока нельзя указывать, напр. Throwable[] в recordExceptions у circuit breaker:
https://st.yandex-team.ru/MARKETDX-84

{% endnote %}

```yaml
clients:
  fault_tolerance_presets:
    circuit_breakers:
      my_circuit_breaker_1:
        failureRateThreshold: 30
        slidingWindowType: TIME_BASED
      my_circuit_breaker_2:
        failureRateThreshold: 25
      retries:
        my_retry:
        max_attempts: 3
      rate_limiters:
        my_rate_limiter:
        limit_refresh_period_millis: 666
      timeouts:
        my_timeout:
        connect_timeout_millis: 666
        read_timeout_millis: 666
```

### tvm {#tvm-self}
Раздел с настройками tvm

```yaml
tvm:
  id: 123
  sources:
    - 345
    - 657
  destinations:
    - 2028530
    - 224
  env:
    local:
      serverTvmDisabled: true
      clientsTvmDisabled: true
    testing:
      id: 234
    production:
      id: 345
```

#### id
tvm id сервиса

#### sources
Список tvm id сервисов, которым разрешен доступ к вашему сервису.

#### destinations
Список tvm id сервисов, куда этот сервис планирует ходить. Для сервисов, клиенты к которым были сгенерированы в разделе `clients`, tvm id здесь указывать не обязательно, они подхватятся из настроек клиентов.

#### serverTvmDisabled
Отключение tvm на серверной части (контроллерах) сервиса. Бывает полезно для отладки в среде `local`

#### clientsTvmDisabled 
Отключение tvm на сгенерированных клиентах сервиса. Бывает полезно для отладки в среде `local`

### modules
Раздел для указания модулей кода, которые необходимо подключить.
Доступные модули:
* [postgres](../../features/postgres.md)
* [mongo](../../features/mongo.md)
* [quartz](../../features/quartz.md)
* [logbroker](../../features/logbroker.md)
* [resilience4j](../../features/resilience4j.md)
* [yt](../../features/yt.md)
* [healz](../../features/healz.md)

Каждый модуль основан на spring boot starter и может быть полностью сконфигурирован в `service.yaml` в соответствующем блоке.

При добавлении модулей, в код добавляются соответствующие проперти в папку properties.d, а так же зависимости в папку ya.make.modules. В ya.make проекта добавится строчка подключения этих зависимостей.

### generation_settings
Раздел для указания настроек генерации.
Подробнее [здесь](../../features/generation_settings.md#Настройка-генерации-исходников).

#### ya_make_dependencies
Отвечает за генерацию зависимостей для модулей

#### modules_templates
Отвечает за генерацию шаблонного кода/тестов модулей

#### api_service_classes
Отвечает за генерацию заглушек реализации ручек


