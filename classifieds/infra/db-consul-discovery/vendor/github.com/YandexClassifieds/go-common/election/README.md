# Distributed Leader Election

## How to use

```go
import github.com/YandexClassifieds/go-common/election/consul

func main(){
    ...
    election, err := consul.Init()
    // check err
    if election.IsLeader() {
        ...
    }
}
```

## Environment

- [_DEPLOY_SERVICE_NAME](https://docs.yandex-team.ru/classifieds-infra/deploy/default-env#_DEPLOY_SERVICE_NAME)
- [_DEPLOY_ALLOC_ID](https://docs.yandex-team.ru/classifieds-infra/deploy/default-env#_DEPLOY_ALLOC_ID)
- COMMON_CONSUL_TOKEN

## Options

### WithNamespace

Нужен при использовании нескольких реализаций в приложении для избежания коллизии.

```go
election1, _ := consul.Init(WithNamespace("service1"))
election2, _ := consul.Init(WithNamespace("service2"))
```

### WithToken

Позволяет явно передать токен. По умолчанию будет использования переменная окружения `COMMON_CONSUL_TOKEN`
```go
election, _ := consul.Init(WithToken(token))
```

### WithTTL

Позволяет задать TTL. По умолчанию используется минимально возможный в 10 секунд.
```go
election, _ := consul.Init(WithTTL(20 * time.Second))
```

### WithConf

Позволяет передать компонент для инициализации приложения (чтения переменных окружения). [Подробнее](go-common/conf)

```go
election, _ := consul.Init(WithConf(conf))
```

### WithAddress

Позволяет задать пользовательский адрес. Полезно для написания тестов и использования consul в docker.
По умолчанию `consul-server.service.common.consul:8500`.

```go
election, _ := consul.Init(WithAddress(address))
```
