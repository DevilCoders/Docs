## ymod_tvm
### Описание
Это модуль для работы с [TVM2](https://wiki.yandex-team.ru/passport/tvm2/), предоставляющий следующие возможности:
* фоновое обновление ключей и тикетов в TVM API;
* синхронное и асинхронное получение тикетов по настраиваемым именам сервисов;
* проверка сервисных и клиентских тикетов;
* отложенный запуск приложения до получения тикетов и ключей;
* интеграция с ymod_httpclient для автоматического добавления заголовка x-ya-service-ticket.

### Конфигурация
#### Базовая конфигурация
```yaml
-   _name: tvm
    system:
        name: tvm
        factory: ymod_tvm::tvm2::impl
    configuration:
        my_tvm_id: 1234567                   # tvm-id сервиса
        tvm_host: tvm-api.yandex.net         # хост tvm-api
        keys_update_interval: 24:00:00       # интервал обновления ключей, рекомендуется не реже раза в сутки
        tickets_update_interval: 01:00:00    # интервал обновления тикетов, рекомендуется не реже раза в час
                                             # (актуальные рекомендации можно найти в документации TVM2)
        retry_interval: 00:10:00             # интервал повтора, если не удалось получить ключи/тикеты
        wait_first_update_on_start: true     # задержка старта приложения до загрузки тикетов
        destinations:                        # сервисы, для которых нужны тикеты
        -   id: 1234568                      # - tvm-id сервиса
            name: friendly_service_name      # - friendly-name для использования в коде
            host: myhost.yandex.net          # - хост для автоматической отправки заголовка x-ya-service-ticket (см ниже)
        -   id: blackbox                     # для blackbox можно не указывать id, поддерживаются также
                                             # blackbox-test, blackbox-corp, blackbox-corp-test, blackbox-stress, blackbox-mimino
        secret_file: /etc/service/tvm_secret # файл с секретом tvm
        secret: ABCDEFQWERTY                 # или секрет
```
#### Вынос общей части конфигурации
Для удобства можно вынести информацию о сервисах (имя, id, host) в отдельный файл, например, mappings.yml:
```yaml
config:
    mappings:
        service1-tst: { id: 123, host: service1-tst.yandex.net }
        service1-corp: { id: 124, host: service1-corp.yandex.net }
        service1: { id: 125, host: service1.yandex.net }
        service2-tst: { id: 234 }
        service2-corp: { id: 235 }
        service2: { id: 236 }
```
В основном конфиге можно подключить mappings.yml и использовать в настройках указанные в нём имена:
```yaml
-   _name: tvm
    configuration:
        include: { _file: path/mappings.yml }
        my_tvm_id: service2
        destinations: [service1, service1-corp]
```

### Использование
#### Найти модуль yplatform
```cpp
#include <ymod_tvm/module.h>
#include <yplatform/find.h>

void test()
{
    auto mod_tvm = yplatform::find<ymod_tvm::tvm2_module>("module_name");
}
```
#### Создать standalone-модуль
```cpp
#include <ymod_tvm/tvm.h>

void test()
{
    ymod_tvm::settings settings;
    // Setup settings...
    ymod_tvm::tvm mod_tvm(settings);
}
```
#### Подписаться на service ticket
```cpp
    mod_tvm.subscribe_service_ticket("my_service", [] (auto& error, auto& ticket) {
        if (error) {
            std::cout << "can't get ticket: " << error.message() << "\n";
        } else {
            std::cout << "ticket is " << ticket << "\n";
        }
    });
    mod_tvm.start();
```
#### Подписаться на готовность всех тикетов
```cpp
    mod_tvm.subscribe_all_tickets_are_ready([] () {
        // Do something.
    });
    mod_tvm.start();
```
#### Подписаться на готовность всех ключей
```cpp
    mod_tvm.subscribe_keys_loaded([] () {
        // Do something.
    });
    mod_tvm.start();
```
#### Получить тикет для сервиса
```cpp
    std::string ticket;
    auto err = mod_tvm.get_service_ticket("my_service", ticket);
    if (err) {
        std::cout << "can't get ticket: " << err.message() << "\n";
    } else {
        std::cout << "ticket is " << ticket << "\n";
    }
```
#### Проверить service ticket
```cpp
void handle_request(yplatform::task_context_ptr ctx, const std::string& incoming_ticket)
{
    err = mod_tvm.check_service_ticket(ctx, incoming_ticket);
    if (err) {
        std::cout << "ticket check failed: " << err.message() << "\n";
    } else {
        std::cout << "ticket checked successfully\n";
    }
}
```
#### Проверить user ticket
```cpp
void handle_request(yplatform::task_context_ptr ctx, const std::string& incoming_user_ticket)
{
    err = mod_tvm.check_user_ticket(ctx, TA_BE_PROD, incoming_user_ticket);
    if (err) {
        std::cout << "user ticket check failed: " << err.message() << "\n";
    } else {
        std::cout << "user ticket checked successfully\n";
    }
}
```
### Интеграция с ymod_httpclient
ymod_httpclient может автоматически добавлять заголовок ```X-Ya-Service-Ticket``` при запросах к хостам, сконфигурированным в ymod_tvm. Для этого в конфигурации клиента необходимо указать ```service_ticket_provider```:
```yaml
-   _name: http_client
    configuration:
        service_ticket_provider:
            module: tvm                      # имя модуля tvm
```
Если указать хост в конфиге не получается (например, список хостов генерируется по шаблону), привязать хост к имени сервиса можно в коде:
```cpp
    mod_tvm.bind_host("myservice.yandex.net", "my_service");
    mod_tvm.start();
```