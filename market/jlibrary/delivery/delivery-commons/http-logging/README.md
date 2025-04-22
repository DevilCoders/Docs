# Http logging

### Описание

Библиотека содержит 2 функциональности:

1) Логирование входящих запросов
2) Логирование исходящих запросов (RestTemplate)

Логируется в том числе и тело запроса/ответа

### Как использовать

##### 1. Логирование входящих запросов

Если Spring Boot, то достаточно просто зарегать бин `ServletRequestLoggingFilter`:

```java
    @Bean
    public ServletRequestLoggingFilter servletRequestLoggingFilter() {
        return new ServletRequestLoggingFilter()
                .setServletName("MDB API")
                .setExcludedPaths(Collections.singletonList("/ping"));
    }
```

Если не Spring Boot, то придется добавлять фильтр в `ServletHandler`, пример (xml config) есть в delivery-tracker

##### 2. Логирование исходящих запросов

Если нужно логировать все запросы, то можно создать `RestTemplateLoggingBeanPostProcessor`, 
который добавит интерсепторы в каждый `RestTemplate` в контексте:

```java
    @Bean
    public RestTemplateLoggingBeanPostProcessor restTemplateLoggingBPP() {
        return new RestTemplateLoggingBeanPostProcessor();
    }
```

Если для некоторых запросов не нужно логировать тело, то можно добавить их в фильтр

```java
    @Bean
    public RestTemplateLoggingBeanPostProcessor restTemplateLoggingBPP() {
        return new RestTemplateLoggingBeanPostProcessor(Arrays.asList(
                UriBasedBodyLoggingFilter.create("delivery_city")
                        .setSkipRequests(false)
                        .setSkipResponses(true),
                UriBasedBodyLoggingFilter.create("geo/data/location")
                        .setSkipRequests(false)
                        .setSkipResponses(true)), null);
    }
```

Если логирование нужно не для всех исходящих запросов, а только для некоторых,
то можно самому сконфигурить `RestTemplate`, добавив в него `LoggingClientRequestInterceptor`

```java
    @Bean
    public LoggingClientRequestInterceptor loggingClientRequestInterceptor() {
        return new LoggingClientRequestInterceptor("MarschrouteClient",
                Arrays.asList(
                        UriBasedBodyLoggingFilter.create("delivery_city")
                                .setSkipRequests(false)
                                .setSkipResponses(true),
                        UriBasedBodyLoggingFilter.create("geo/data/location")
                                .setSkipRequests(false)
                                .setSkipResponses(true))
        );
    }

    @Bean
    public RestTemplate loggingRestTemplate(LoggingClientRequestInterceptor interceptor) {
        return new RestTemplateBuilder()
                .setConnectTimeout(CONNECT_TIMEOUT)
                .setReadTimeout(READ_TIMEOUT)
                .interceptors(interceptor)
                .build();
    }
```

### Примечание

В классы `RestTemplateLoggingBeanPostProcessor`, `LoggingClientRequestInterceptor` и `ServletRequestLoggingFilter`
можно передать список дополнительных логгеров, если хочется добавить какой-нибудь кастомный логгер

Для этого нужно реализовать интерфейс HttpLogger и передать логгер в конструкторы

Это может пригодиться в mdb, где используется `TskvLogger` для этих целей


