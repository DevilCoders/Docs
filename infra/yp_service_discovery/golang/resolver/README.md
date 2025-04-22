#### Go YP Service Discovery resolver

[[godoc](https://godoc.yandex-team.ru/pkg/a.yandex-team.ru/infra/yp_service_discovery/golang/resolver/)] [[yp sd docs](https://wiki.yandex-team.ru/yp/discovery/usage/)]

Реализация резолвера YP Service Discovery на Go. Позволяет получать инфромацию о хостах, находящихся в YP, по Endpoint set или Pod set.

В основе лежит интерфейс `Resolver`, описывающий необходимые методы для реализации резолвера. На данный момент существует две реализации:

- [httpresolver](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/golang/resolver/httpresolver) - резолвер на основе HTTP клиента
- [grpcresolver](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/golang/resolver/grpcresolver) - резолвер на основе gRPC клиента

### Примеры

Инициализация клиента и запрос данных эндпоинтов в кластере `SAS`:

```go
package main

import (
    "context"
    "log"

    "a.yandex-team.ru/infra/yp_service_discovery/golang/resolver"
    "a.yandex-team.ru/infra/yp_service_discovery/golang/resolver/httpresolver"
)

func main() {
    r, err := httpresolver.New()
    if err != nil {
        log.Fatal(err)
    }

    ctx := context.Background()
    resp, err := r.ResolveEndpoints(ctx, resolver.ClusterSAS, "chaos-service")
    if err != nil {
        log.Fatal(err)
    }

    log.Println(resp.ResolveStatus)
}
```

Инициализация с дополнительными параметрами:

```go
package main

import (
    stdlog "log"

    "a.yandex-team.ru/infra/yp_service_discovery/golang/resolver"
    "a.yandex-team.ru/infra/yp_service_discovery/golang/resolver/httpresolver"
    "a.yandex-team.ru/library/go/core/log"
    "a.yandex-team.ru/library/go/core/log/zap"
)

func main() {
    // все запросы будут идти на балансер YP SD в кластере SAS
    serviceURL := "http://" + resolver.ServiceDiscoveryBalancerSAS + ":" + resolver.ServiceDiscoveryHTTPPort

    // устанавливаем кастомный логгер
    logger := zap.Must(zap.CLIConfig(log.InfoLevel))

    r, err := httpresolver.New(
        httpresolver.WithServiceURI(serviceURL),
        httpresolver.WithLogger(logger),
    )
    if err != nil {
        stdlog.Fatal(err)
    }

    ...
}
```

#### Кеширующий резолвер

Существует реализация кеширующего враппера над реализацией интерфейса `Resolver` - [cachedresolver](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_service_discovery/golang/resolver/cachedresolver).
Использование данного враппера позволяет уменьшить количество хождений в сеть, а также сократить время ответа и возможность появления ошибки при запросе данных у YP SD.

Пример:

```go
package main

import (
    "context"
    "time"

    "a.yandex-team.ru/infra/yp_service_discovery/golang/resolver"
    "a.yandex-team.ru/infra/yp_service_discovery/golang/resolver/cachedresolver"
    "a.yandex-team.ru/infra/yp_service_discovery/golang/resolver/cacher"
    "a.yandex-team.ru/infra/yp_service_discovery/golang/resolver/httpresolver"
)

func main() {
    // для правильной работы врапперу необходимы резолвер и кешер
    r, _ := httpresolver.New()
    // время жизни объекта в кеше не будет превышать 10 секунд
    c := cacher.NewInMemory(cacher.InMemoryObjectTTL(10 * time.Second))

    // данная опция позволяет использовать объект из кеша с истекшим сроком жизни
    // в случае если произошла ошибка при запросе к YP SD
    useStaleCache := cachedresolver.ReturnStaleCache(true)

    cr, _ := cachedresolver.New(r,c, useStaleCache)

    ctx := context.Background()
    resp, err := cr.ResolveEndpoints(ctx, resolver.ClusterSAS, "chaos-service")
    ...
}
```

#### Получение данных всех эндпоинтов

Текущая реализация интерфейса `Resolver` позволяет получать данные только в одном кластере.
Для получения данных во всех кластерах следует использовать список `resolver.AvailableClusters`.

Пример:
```go
package main

import (
    "context"
    "log"

    "a.yandex-team.ru/infra/yp_service_discovery/golang/resolver"
    "a.yandex-team.ru/infra/yp_service_discovery/golang/resolver/httpresolver"
)

func main() {
    r, _ := httpresolver.New()

    var endpoints []*resolver.Endpoint
    for _, cluster := range resolver.AvailableClusters {
        ctx := context.Background()
        resp, err := r.ResolveEndpoints(ctx, cluster, "chaos-service")
        if err != nil {
            log.Fatal(err)
        }

        if resp.ResolveStatus != resolver.StatusEndpointNotExists &&
            resp.EndpointSet != nil {
            endpoints = append(endpoints, resp.EndpointSet.Endpoints...)
        }
    }

    ...
}
```
