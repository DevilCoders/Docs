# logctl

## Что это?

Консольная утилита для конфигурации поставки логов в YT.

## Требования

- Python3
```(bash)
python3 -m pip install -r requirements.txt
```
- [arc](https://docs.yandex-team.ru/arc/)
- [logbroker cli](https://logbroker.yandex-team.ru/docs/interfaces/cli)

## Использование

Чтобы настроить поставку новых логов, нужно:
1. [Создать аккаунт](https://logbroker.yandex-team.ru/docs/how_to/create_account) в логброкере, либо убедиться что он уже создан (временное ограничение)
1. Подготовить конфиг (см. ниже)
1. Выполнить команду `logctl apply <dir-with-config>` (подробности в `logctl --help`)
1. Влить сгенерированный ПР с настройками логфеллера и пушклиента
1. Дождаться пока [выкатится логфеллер](https://wiki.yandex-team.ru/logfeller/faq/#jaizmenilnastrojjkilogakogdaoniprorastut) и в YT появятся новые таблицы
1. Выкатить сервис с обновленным конфигом пушклиента

## Конфигурация
### Описание конфига

Приложение и его логи описываются в файле `service.yml`:

```(yaml)
config:
    app: hello-world-app
    envs: ["production"]
    tvm_id:
        production: <production-tvm-id>
    log_settings:
        topic: mail-{app}/{app}-{log}-log # Можно использовать шаблонизацию (см. описание ниже).
        fs_log_path: /var/log/{app}/{log}.log # Путь до файла с логом на конечной машине.
        tvm_secret_path: /etc/{app}/tvm_secret # Путь до файла с TVM секретом на конечной машине.
        push_client_config_path: deploy/etc/statbox-push-client/main.yaml # Относительный путь до конфига пушклиента в репозитории.
        push_client_log_options: # Опциональный параметр. Произвольные дополнительные опции, которые нужно пробросить в конфиг пушклиента.
            compress: zstd # Например, можно переопределить метод сжатия.
        time_format: "%Y-%m-%d %H:%M:%S" # Формат поля "timestamp" в логе.
        logfeller_log_name: mail-{app}-{log}-log # Совпадает с именем таблицы в YT.
        logfeller_parser_name: {app}-{log}-log # Можно настроить для совместимости с существующими парсерами.
        logfeller_logs_config_name: mail_hahn_logs # Для всех почтовых проектов следует использовать "mail_hahn_logs".
        logfeller_streams_config_name: mail_hahn_streams # Для всех почтовых проектов следует использовать "mail_hahn_streams".
        periods: # Опциональный параметр. Периоды агрегации логов. По умолчанию используются периоды 1 день и 30 минут.
         - name: 1d
           lifetime: 365d
    logs:
      - name: access
        fields: ["status_code", "request", "y_context", "x_request_id"]
```

В настройках логов можно использовать шаблонизацию: вместо `{app}` в данном примере подставится `hello-world-app`, вместо `{env}` - `production`, а вместо `{log}` - `access`.

Для лога можно указать неполный список полей. Недостающие поля либо будут выведены из первых нескольких строк лога, либо попадут в колонку `_other` в YT.

По умолчанию все поля имеют тип `string`. Отличные от `string` типы нужно указывать в суффиксе (например, `fields: ["status_code:int64"]`). Список дополнительных типов: `bool`, `int64`, `uint64`, `double`, `ts` (timestamp).

Если какие-то настройки из секции `log_settings` не подходят для конкретного лога, их можно перезаписать. Например:

```(yaml)
logs:
  - name: httpout
    fields: ["type","status","reason","y_context"]
    fs_log_path: /var/log/hello-world-app/httpout.log
```

### Наследование конфигов
Общие настройки можно вынести в базовый конфиг:

```(yaml)
config:
    log_settings:
        topic: mail-{app}/{app}-{log}-log
        fs_log_path: /var/log/{app}/{log}.log
        push_client_config_path: deploy/etc/statbox-push-client/main.yaml
        logfeller_log_name: mail-{app}-{log}-log
        logfeller_parser_name: "{app}-{log}-log"
        logfeller_logs_config_name: mail_hahn_logs
        logfeller_streams_config_name: mail_hahn_streams
```

Тогда конфиг конечного приложения будет выглядеть так:

```(yaml)
base: mail/hello-world-app/base.yml # Задается от корня аркадии.
config:
    app: hello-world-app
    envs: ["production"]
    tvm_id:
        production: <production-tvm-id>
    logs:
      - name: access
        fields: ["status_code", "request", "y_context", "x_request_id"]
```
