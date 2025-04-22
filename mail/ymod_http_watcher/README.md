# ymod_http_watcher

## Описание
Модуль предназначен для настройки регулярного выполнения HTTP-запроса (GET) и передачи результата кастомному обработчику.
В качестве HTTP-клиента используется [yhttp::cluster_client](https://a.yandex-team.ru/arc/trunk/arcadia/mail/ymod_httpclient)

## Пример конфигурации модуля
```yaml
module:
-   _name: http_watcher
    system:
        name: http_watcher
        factory: NYmodHttpWatcher::TWatcher
    configuration:
        reactor: global
        url: "/metadata"
        period: 10s         # переодичность запроса
        start_delay: 1s     # стартовая задержка
        http_client:
            # Стандартные настройки cluster_client
            # ...
```
