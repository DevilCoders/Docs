Библиотека logbroker-manager
============================

Данная библиотека предоставляет реализацию клиента для конфигурирования аккаунта в logbroker.

Конфигурация
------------

Для начала необходимо сконфигурировать менеджер:

```yaml
logbroker:
  manager:
    operation-timeout: 1m # таймаут операций клиента
    token: ... # (опционально) OAuth-токен для аутентификации
```

Если `OAuth-токен` не задан, то будет выполнена процедура поиска, описанная [тут](java_micronaut_logbroker_manager.md#oauth).

Также для создания клиента нам необходимо сконфигурировать `grpc`-канал. Каналы могут быть использованы как по одному на клиент, так и один канал на несколько клиентов. Конфигурация задается в конфиге ([подробности](https://micronaut-projects.github.io/micronaut-grpc/2.0.5/guide/index.html#client)):

```yaml
grpc:
  channels:
    manager:
      plaintext: true
      max-retry-attempts: 3
      address: ${logbroker.installation.logbroker.management-host}:${logbroker.installation.logbroker.management-port}
```

Для доступа к параметрам инсталляций из конфига доступны следующие переменные:

- `logbroker.installation.%installation-name%.management-host` - хост api управления инсталляции
- `logbroker.installation.%installation-name%.management-port` - порт api управления инсталляции
- `logbroker.installation.%installation-name%.host` - хост api записи/чтения инсталляции
- `logbroker.installation.%installation-name%.port` - порт api записи/чтения инсталляции

`installation-name` - имя инсталляции `logbroker` из перечисления `LogbrokerInstallation`.

Клиент
------

Объект клиента можно обменять на `grpc`-канал у бина `ManagerClientFactory`:

```java
import java.util.List;
import javax.inject.Inject;
import javax.inject.Singleton;
import io.micronaut.grpc.annotation.GrpcChannel;
import ru.yandex.payments.micronaut_logbroker.manager.ManagerClient;
import ru.yandex.payments.micronaut_logbroker.manager.ManagerClientFactory;

@Singleton
class MyBean {
    private final ManagerClient client;

    @Inject
    public MyBean(ManagerClientFactory factory,
                  @GrpcChannel("manager") // указываем имя канала из конфига
                  ManagedChannel channel) {
        this.client = factory.getClient(channel);
    }

    public void doSomething() {
        // команды на изменение параметров аккаунта лучше всего отсылать батчем
        client.execute(List.of(
            client.deleteConsumer("myConsumer"),
            client.deleteTopic("topic")
        )).block();
    }
}
```
