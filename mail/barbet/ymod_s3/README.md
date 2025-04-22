# ymod_s3

## Что это?

Модуль обертка над официальным [S3 SDK](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/libs/aws-sdk-cpp/aws-cpp-sdk-s3).

## Реализация
На текущий момент модуль использует под капотом **синхронный** `curl http` клиент, `reactor` в качестве пула потоков и `logger` для логгирования.

## Настройки

### Логи и реактор
Логи пишутся в tskv формате с помощью `logdog`.

```
logger: name_of_logger     # имя логера в платформе
log_level: Off             # уровень логирования aws клиента 
# настраивается отдельно от логгера, см. Aws::Utils::Logging::LogLevel
reactor: global            # реактор для запуска
```

### Credentials
Поддерживаются следующие форматы:
```
logger: global
...
credentials:
    simple:
        access_key_id: key_id
        secret_key: key
        session_token: token
```
```
credentials:
    tvm:
        module: name_of_tvm_module
        s3_id: id_of_s3_service
        service_id: id_of_current_service
```

### Клиент
```
client:
    user_agent: barbet # string
    scheme: HTTP # value from enum Aws::Http::Scheme
    endpoint_override: storage-int.mdst.yandex.net:80
    # string host:port

    connect_timeout_ms: 1000
    request_timeout_ms: 1000

    region: '' # optional, string
    sign_payloads: Never
    # optional, Aws::Client::AWSAuthV4Signer::PayloadSigningPolicy
    ca_path: '/etc/ssl/certs/' # optional, string 
    
    use_virtual_addressing: false # optional, bool
```

