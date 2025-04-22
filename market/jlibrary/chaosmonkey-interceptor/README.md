Ticket: https://st.yandex-team.ru/MARKETPROJECT-6536

# Описание
С помощью реарр флагов до целевого сервиса доносим команду о внесении ошибки в контекст обработки запроса.

## Общий вид
В headers запроса будем присылать параметры для внесения ошибок. Это общий формат реарров, поэтому нужно самостоятельно парсить query и искать реарр для себя

```
rearr-factors: enable_simple_return_by_post=1;service1-chaosmonkey-500;service2-chaosmonkey-500=1;market_white_cpa_on_blue=2;service3-chaosmonkey-timeout=10000
```

**должно работать только в тестинге** в противном случае этим можно положить продакшен сервис

## 4xx/5xx
```
rearr-factors=<service_name>-chaosmonkey-500=1
rearr-factors=<service_name>-chaosmonkey-400=1
```

<service_name> - название вашего сервиса
значение = 1 – ответить 400 или 500. Остальные значения нужно игнорировать

## Повышенные тайминги
```rearr-factors=<service_name>-chaosmonkey-timeout=<timeout_in_millis>```

<service_name> - название вашего сервиса
<timeout_in_millis> - будет приходить от потребителя. Максимальное значение ограничить в 10000мс

# Правила подключения
В проперти приложения прописываем
```
chaosmonkey.service-name=<Название вашего сервиса>
chaosmonkey.profiles={<название профилей приложения на которых обезьяна будет работать>}
chaosmonkey.rearr-header-name=<Название хедера в котором передаются rearr factors>
```
### Если Java config:
См. `ChaosMonkeyTestConfig` как пример:
1. implements `WebMvcConfigurer`.
2. `@EnableWebMvc` в проекте на конфиге/в конфиге уровнем выше
3. `@Import(ChaosMonkeyInterceptorConfig.class)`
### Если XML-конфигурация
добавляем бин `ChaosMonkeyInterceptorConfig` и `mvc:interceptor`
```
    <bean class="ru.yandex.market.handler.interceptor.ChaosMonkeyInterceptorConfig"/>
    <mvc:interceptors>
        <ref bean="chaosMonkeyHandlerInterceptor"/>
    </mvc:interceptors>
```

## Пример подключения
```
chaosmonkey.service-name=loyalty
chaosmonkey.profiles={'testing'}
chaosmonkey.rearr-header-name=X-Market-Rearrfactors
```
