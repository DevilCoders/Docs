# Модуль resilience4j
Модуль позволяет подключить и настроить инструменты resilience4j для использования их в любом месте в своем коде.

## Настройка
Настройка происходит в `service.yaml`
Пример конфига service.yaml:
```yaml
modules:
  resilience4j:
    circuitbreaker:
      instances:
        backendA:
          registerHealthIndicator: true
          slidingWindowSize: 100
        backendB:
          registerHealthIndicator: true
          slidingWindowSize: 10
          permittedNumberOfCallsInHalfOpenState: 3
          slidingWindowType: TIME_BASED
    retry:
      instances:
        backendA:
          maxAttempts: 3
          waitDuration: 10s
          enableExponentialBackoff: true
          exponentialBackoffMultiplier: 2
    ratelimiter:
      instances:
        backendA:
          limitForPeriod: 10
          limitRefreshPeriod: 1s
          timeoutDuration: 0
          registerHealthIndicator: true
          eventConsumerBufferSize: 100
        backendB:
          limitForPeriod: 6
          limitRefreshPeriod: 500ms
          timeoutDuration: 3s           
```

Список доступных модулей resilience4j и параметров можно посмотреть [на этой странице](https://resilience4j.readme.io/docs/getting-started-3#configuration).

## Использование в коде
Использовать модули в коде можно с помощью аннотаций. Подробнее можно почитать [здесь](https://resilience4j.readme.io/docs/getting-started-3#annotations).
```java
@CircuitBreaker(name = BACKEND, fallbackMethod = "fallback")
@RateLimiter(name = BACKEND)
@Bulkhead(name = BACKEND)
@Retry(name = BACKEND, fallbackMethod = "fallback")
@TimeLimiter(name = BACKEND)
public Mono<String> method(String param1) {
    return Mono.error(new NumberFormatException());
}

private Mono<String> fallback(String param1, IllegalArgumentException e) {
    return Mono.just("test");
}

private Mono<String> fallback(String param1, RuntimeException e) {
    return Mono.just("test");
}
```

## Использование rate limiter в генерируемых контроллерах
Есть возможность указания rate limiter для сгенерированных контроллеров через [api.yaml](../how_it_works/configuration/api_yaml.md#rate-limiter).