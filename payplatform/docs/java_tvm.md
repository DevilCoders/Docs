# Библиотека tvm

Библиотека обеспечивает поддержку в micronaut возможностей TVM.

## Конфигурация

Чтобы включить tvm, необходимо добавить следующие опции в yml конфиге:

```yaml
micronaut:
    security:
        enabled: true # By default is true, make sure that it's not switched to false
    http:
        services:
            tvm-tool:
                urls:
                    - http://localhost:2 # The tvmtool url
tvm2:
  token: "Your token"
  services: # service tvm ids we send requests to
    self: 42
  allowed-clients: # service tvm ids we handle requests from
    self: 42
```

Следует обратить внимание, что по умолчанию `micronaut.security.enabled` выставлен в `true` в Micronaut. Это влечет за собой две вещи:

* Если поддержка tvm не предполагается, то нужно выставить ее явно в false, в противном случае же не забыть прописать `tvm2.token`.
* Нельзя включить `micronaut.security.enabled`, и при этом не указать токен, так как тогда все приложение будет падать со сбоем из-за `TvmAnnotationRule`. Так сделано специально, чтобы разработчик не мог завести новое приложение без поддержки TVM.

## Поддержка в контроллерах

Предположим, что нужно обеспечить обращение с заголовками TVM для конкретной ручки в проекте (то есть обращаются к приложению, а не само приложение лезет куда-то). Для начала, идентификаторы того приложения, которое собирается обращаться к сервису, нужно прописать в `tvm2.allowed-clients`. Им можно давать произвольные названия, например:

```yaml
tvm2:
    allowed-clients:
        service-a: 100500
        service-b: 9000
```

Далее, на нужную ручку нужно повесить аннотацию `TvmSecured` (если все ручки контроллера должны быть покрыты TVM, то данную аннотацию можно навесить сразу на весь класс контроллера). Если же предполагается, что ручке надо передать пользовательский тикет, то нужно указать аргумент типа `Uid`, аннотированный `@TvmUser`. Вот пример с двумя ручками:

```java
@Controller
class ExampleController {
    @TvmSecured
    @Get("/general-handle")
    public String generalHandle() {
        // ...
    }

    @TvmSecured
    @Get("/user-handle")
    public String userHandle(@TvmUser Uid uid) {
        // ...
    }
}
```

## Поддержка в клиентах

Если в приложении необходимо обращаться к другим сервисам, то для начала эти другие сервисы нужно прописать в `application.yaml`.

```yaml
tvm2:  
  services: # service tvm ids we send requests to
    service-a: 100500
    service-b: 9000
```

Затем нужно сделать клиента, который будет обращаться к сервисам, чтобы он добавлял дополнительный заголовок сервисного тикета (а если нужно, то и пользовательского тикета). Для этого можно воспользоваться той же аннотацией `TvmSecured`:

```java
@TvmSecured
@Client(id = ServiceAClient.ID)
interface ServiceAClient {
    String ID = "service-a";

    @Get("/serviceHandle")
    String serviceHandle();

    @Get("/userHandle")
    String user(@Header(TVM_USER_TICKET_HEADER) String userTicket);
}
```

Здесь для сервиса используется алиас из `application.yml`, а не числовой идентификатор. Это чтобы приложение могло работать на разных стендах и окружениях, используя один алиас.
