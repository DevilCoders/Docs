# Аутентификация

## Включение поддержки аутентификации в своём сервисе
Для включения аутентификации нужно импортировать конфигурацию ```ru.yandex.market.wms.auth.core.configuration.AuthConfiguration```
и включить её флагом ```check.authentication: 'default'``` в ```application.properties```

## Фильтры

Аутентификация реализована как цепочка фильтров, применяемых к каждому запросу. Фильтры конфигурируются в
[InforAuthSecurityConfiguration](https://a.yandex-team.ru/arc_vcs/market/logistics/wms/app/auth-core/src/main/java/ru/yandex/market/wms/auth/core/configuration/InforAuthSecurityConfiguration.java).

### LgwTokenAuthenticationFilter
Первый фильтр, применяется для аутентификации по токену в теле xml-запроса. Нужен для поддержки формата
аутентификации [logistics-api](https://yandex.ru/dev/market/fulfillment/doc/dg/concepts/format.html).

Токен задаётся в application.security.lgw-token и подставляется из секрета LgwApiToken (указан в
common-spring/src/main/resources/application-fragment-common.yml)

Фильтр применяется только для ручек, указанных в параметре ```application.security.token-security-methods```

**Пример**
```yml
application:
  security:
    token-secured-methods: /*/order-status,/*/order-status-history,/*/inbound/get-inbound-details,/*/return-inbound/get-return-inbound-details,/*/registers
```

{% note warning %}

Фильтр актуален пока в API есть ручки, в которые LGW ходит напрямую, миную ServiceBus. После перевода всех этих ручек
на ServiceBus фильтр нужно удалить.

{% endnote %}

### InforCookieAuthenticationFilter
Аутентификация по куке старого Infor %%com.epiphany.SessionID%%. Используется для того чтобы пользователи, залогиненные
в старом интерфейсе могли прозрачно отправить запрос в одно из новых приложений.
Когда пользователь приходит с кукой SessionID, то из куки берётся логин, дата выдачи куки и срок действия.
Если пользователь с таки логином существует в LDAP и срок действия куки не истек, то выдается JWT-токен.

### JwtAuthenticationFilter
Аутентификация с [JWT](https://jwt.io/) токеном используется для проверки доступа пользователей. При входе в систему
через ручку /login сервиса Auth пользователю выдаётся JWT-токен. Каждый запрос к серверу должен содержать этот токен
в заголовке Authoriztion. Каждый ответ сервера содержит перевыпущенный или тот же токен в заголовке.

Токен содержит в себе имя пользователя, список ролей, дату выпуска и время жизни. Токен действителен одну минуту (параметр
YM_AUTH_TOKEN_TTL). Если время жизни не истекло, сервис доверяет токену. Если время жизни истекло, сервис делает запрос
checkToken в сервис Auth и получает новый токен.  При неактивности пользователя более 15 минут (параметр
YM_AUTH_TTL_MINUTES), токен не перевыпускается, от пользователя требуется повторная аутентификация.

### InforTvmAuthenticationFilter
Аутентификация при обращении из одного сервиса к другому через [TVM](https://wiki.yandex-team.ru/passport/tvm2/)
```yaml
application:
  security:
    use-tvm-auth: true
check:
    authentication: 'default'
```
В паспортах ABC участвующих сервисов должны быть по 3 TVM приложения (для создания понадобится роль TVM менеджер):
1. ```market_wms_<service-name>_testing```
2. ```market_wms_<service-name>_prestable```
3. ```market_wms_<service-name>_prod```

Секреты должны быть добавлены в соответствующие конфигурации окружений в секретнице с названием ```<ServiceName>TvmSecret```.

Переменная вида ```<ServiceName>TvmSecret={{ <ServiceName>TvmSecret }}``` должна быть добавлена в [common.properties](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/wms-init/properties/common.properties).

Также туда необходимо добавить переменную ```<ServiceName>CacheTvmDir=/var/cache/<service-name>/tvm/```, а в
run-wms-template.sh сервисов:
```shell
TVM_CACHE_DIR="/var/cache/<service-name>/tvm"
mkdir -p $TVM_CACHE_DIR
```

В остальные [properties-файлы SRE](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/wms-init/properties) нужно добавить соответствующие ID TVM приложений (ID ресурса в ABC)
в виде ```<ServiceName>ServiceId=<tvm-id>```.

Пример TVM конфигурации авторизующегося сервиса (servicebus в api):
```java
@Configuration
@ParametersAreNonnullByDefault
public class TvmConfiguration {

    @Value("${servicebus.tvm.serviceId}")
    private int servicebusTvmServiceId;

    @Value("${servicebus.tvm.secret}")
    private String servicebusTvmSecret;

    @Value("${wms.api.tvm.serviceId}")
    private int apiTvmServiceId;

    @Value("${servicebus.tvm.cache.dir}")
    private String cacheTvmDir;

    @Bean
    @Profile({Profiles.PRODUCTION, Profiles.TESTING})
    @Primary
    public TvmClient tvmClient() {
        TvmApiSettings tvmApiSettings = new TvmApiSettings()
                .setSelfTvmId(servicebusTvmServiceId)
                .enableServiceTicketsFetchOptions(
                        servicebusTvmSecret,
                        new int[] {
                                SqsJmsConfiguration.SQS_PRODUCTION_ID,
                                apiTvmServiceId
                        }
                ).enableServiceTicketChecking()
                .setDiskCacheDir(cacheTvmDir);

        return new NativeTvmClient(tvmApiSettings);
    }

    @Bean
    @Profile({Profiles.TEST, Profiles.DEVELOPMENT})
    public TvmClient tvmClientMock() {
        return new TvmClientMock();
    }

    @Bean
    @Profile({Profiles.TEST, Profiles.DEVELOPMENT})
    @Qualifier("apiTvmTicketProvider")
    public TvmTicketProvider apiTvmTicketProviderMock() {
        return new TvmTicketProviderStub();
    }
}
```
```yaml
wms:
  api:
    tvm:
      serviceId: ${ApiTvmServiceId}
servicebus:
  tvm:
    serviceId: ${ServicebusTvmServiceId}
    secret: ${ServicebusTvmSecret}
    cache:
      dir: ${ServicebusCacheTvmDir}
```
Пример авторизующего сервиса (api):
```java

public class ApiSecurityConfiguration {

    @Configuration
    @Conditional(TvmCondition.class)
    public static class ApiTvmConfiguration {

        @Value("${api.tvm.serviceId}")
        private int apiTvmServiceId;

        @Value("${api.tvm.secret}")
        private String apiTvmSecret;

        @Value("${servicebus.tvm.serviceId}")
        private int serviceBusTvmServiceId;

        @Value("${api.tvm.cache.dir}")
        private String cacheTvmDir;

        @Bean
        @Primary
        @Profile({Profiles.PRODUCTION, Profiles.TESTING})
        public TvmClient tvmClient() {
            TvmApiSettings tvmApiSettings = new TvmApiSettings()
                    .setSelfTvmId(apiTvmServiceId)
                    .enableServiceTicketsFetchOptions(
                            apiTvmSecret,
                            new int[] {
                                    serviceBusTvmServiceId,
                                    SqsJmsConfiguration.SQS_PRODUCTION_ID
                            }
                    ).enableServiceTicketChecking()
                    .setDiskCacheDir(cacheTvmDir);

            return new NativeTvmClient(tvmApiSettings);
        }

        @Bean
        @Primary
        @Profile({Profiles.TEST, Profiles.DEVELOPMENT})
        public TvmClient tvmClientMock() {
            return new TvmClientMock();
        }

        @Bean
        public TvmClientApi tvmClientApi(TvmClient tvmClient) {
            return new TvmClientImpl(tvmClient);
        }

        @Bean
        public TvmTicketChecker tvmTicketChecker(
                @Value("${api.tvm.check-user-ticket:false}") boolean checkUserTicket,
                @Value("${api.tvm.log-only-mode:true}") boolean logOnlyMode,
                @Value("${api.tvm.allowed-service-ids:}") Set<Integer> allowedServiceIds,
                @Value("${api.tvm.api-methods}") Set<String> apiMethods
        ) {
            TvmTicketCheckerImpl checker = new TvmTicketCheckerImpl();
            checker.setCheckUserTicket(checkUserTicket);
            checker.setAllowedServiceIds(allowedServiceIds);
            checker.setApiMethods(apiMethods);
            checker.setLogOnlyMode(logOnlyMode);
            return checker;
        }
    }
}
```
```yaml
application:
  security:
    use-tvm-auth: true
check:
  authentication: 'default'
api:
  tvm:
    serviceId: ${ApiTvmServiceId}
    secret: ${ApiTvmSecret}
    check-user-ticket: false
    log-only-mode: false
    allowed-service-ids: ${ServicebusTvmServiceId}
    api-methods: /*
    cache:
      dir: ${ApiCacheTvmDir}
servicebus:
  tvm:
    serviceId: ${ServicebusTvmServiceId}
```
При необходимости в методы запросов в клиенте необходимо докидывать TVM заголовки, можно использовать [TvmClientUtils](https://a.yandex-team.ru/arc_vcs/market/logistics/wms/app/common-spring/src/main/java/ru/yandex/market/wms/common/spring/tvm/TvmClientUtils.java?rev=r8445883#L13) (например [так](https://a.yandex-team.ru/arc_vcs/market/logistics/wms/app/auth-core/src/main/java/ru/yandex/market/wms/auth/client/AuthClient.java?rev=r8606020#L88)).

При деплое не забываем сначала выкатывать авторизующий сервис.

## Использование в коде
### Получение текущего пользователя
Пользователя можно получить двумя способами.
1. Заинжектить ```SecurityDataProvider securityDataProvider``` и получать его через ```securityDataProvider.getUser```
2. Получать его из ```SecurityContextHolder.getContext().getAuthentication().getPrincipal()```

### Защита отдельных методов
Если требуется ограничить доступ к ручке или методу, можно использовать аннотацию ```@Secured(InforRole.ИМЯ_РОЛИ)```

## Отключение аутентификации для методов
Для отключения аутентификации нужно добавить ручку в unsecured-methods в appliction.properties
```
application:
  security:
    unsecured-methods: /конкретная_ручка,/все_ручки_любого_уровня_вложенности/**,/непосредственные_дочерние_ручки/*
```

Всегда нужно добавлять туда ручки
```
/hc/**
/monitoring/**
/pagematch/**
/swagger-ui/**,/swagger-resources/**,/v3/**
```

## Тесты и аутентификация
Для тестов в ```application-test.yml``` следует указать ```check.authentication: mock```. После это в SecurityContext
всегда будет лежать пользователь **TEST** (из ```TestSecurityDataProvider```)
