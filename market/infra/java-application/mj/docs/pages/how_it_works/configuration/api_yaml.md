# api.yaml
**api.yaml** - файл с описанием API в формате openapi. Этот файл используется для генерации серверной части сервиса (контроллеров), а так же может быть использован другими сервисами для генерации клиентов к вашему сервису.

{% note warning %}

* Файл должен находиться в папке `src/main/resources/openapi/api/`, в противном случае, кастомный путь до файла должен быть указан в [service.yaml](service_yaml.md#serveropenapispecpath)
* Ручки `ping` и `monitoring` указывать в спецификации не нужно.

{% endnote %}

Описание API должно быть реализовано в формате [Open API](https://swagger.io/specification/). Но при использовании с MJ, используются дополнительные поля с префиксом `x-`.

## x-servers
Так как стандартная спецификация Open Api не особо поддерживает указание различных хостов для разных сред, то мы вынесли эту логику в свое поле `x-servers`.
В этом поле можно использовать [механизм указания значений для разных сред](environment.md).

{% note warning %}

Необходимо указывать схему **http** или **https**

{% endnote %}

Пример того, как это может выглядеть:
```yaml
x-servers:
  url: http://localhost:8080
  env:
    testing:
      url: https://my-testing.service.yandex-team.ru
    production:
      url: https://my.service.yandex-team.ru
```

## Rate limiter
Есть возможность использовать rate limiter из модуля [resilience4j](../../features/resilience4j.md) на ручках.

### Дефолтный rate limiter
Можно указать rate limiter для всех ручек контроллера. Для этого нужно указать id нужного rate limiter через следующую настройку в `api.yaml`:
```yaml
x-settings:
  defaultRateLimiter: myRateLimiterId
```

Идентификатор rate limiter указывается в [service.yaml](service_yaml.md#modules). Для примера выше кусок service.yaml мог выглядеть так:
```yaml
modules:
  resilience4j:
    ratelimiter:
      instances:
        myRateLimiterId:
          limitForPeriod: 10
          limitRefreshPeriod: 1s
          timeoutDuration: 0
```

### Rate limiter для конкретных ручек
Для каждой конкретной ручки можно указать свой rate limiter. Этот rate limiter будет у ручки использоваться вместо дефолтного, если такой был указан.
Указание rate limiter для конкретной ручки делается через указания его id в `x-settings.rateLimiter` у этой ручки. Например:
```yaml
paths:
  /helloWorld:
    get:
      tags:
        - helloWorld
      x-settings:
        disableSecurity: true
        rateLimiter: myRateLimiterId
      responses:
        200:
          description: OK
          content:
            text/plain:
              schema:
                type: string
          parameters:
            - name: name
              in: query
              schema:
                type: string
```


## Про tvm
В `api.yaml` можно настраивать различные настройки tvm для отдельных ручек.
* **disableSecurity** - отключение проверки tvm
* **checkUserTicket** - включение проверки наличия user ticket

По-умолчанию, оба значения `false`.

Эти настройки можно применять с [механизмом указания значений для разных сред](environment.md).
```yaml
paths:
  /helloWorld:
    get:
      tags:
        - helloWorld
      x-settings:
        checkUserTicket: true
        env:
          testing:
            disableSecurity: true
      responses: #...
```

## Важное про `tags`
{% note warning %}

Поле `tags` используется для разделения api на разные составные части. Но так же поле `tags` используется при генерации имен классов для клиентов (и разделения этих клиентов). Если тег для ручки указан не будет, то она попадет в клиент с названием `DefaultApi`. Поэтому **максимально настоятельно рекомендуется помечать тегом каждую ручку**.

{% endnote %}
