# TVM

{% note info %}

Ознакомиться с общей информацией о TVM можно [здесь](https://wiki.yandex-team.ru/passport/tvm2/).  

Краткий план действия:  
1. Создать TVM ресурс в ABC вашего сервиса. На выходе вы получите TVM id и секрет, записанные в секретницу.  
2. Секрет из секретницы нужно пробросить в контейнер (инструкция для [Nanny](https://wiki.yandex-team.ru/market/development/java/rtc/#dobavitsekretyizyav) и [Deploy](https://deploy.yandex-team.ru/docs/how-to/secrets#obuyavlenie-sekretov-v-ui))  
3. TVM id указать в service.yaml (следовать текущей инструкции)

{% endnote %}

Для включения поддержки tvm в сервисе на MJ достаточно прописать tvm id этого сервиса в [service.yaml](../how_it_works/configuration/service_yaml.md#tvm-self).

## Возможности
- Проверка `Service Ticket` и `User Ticket` у входящих запросов
- Локальный доступ к тестингу сервисов, написанных на MJ фреймворке (в общем смысле доступ к сервисам, имеющим в sources tvm id [этого сервиса](https://abc.yandex-team.ru/services/market-local-environment-service/).
- Встроенная в клиенты генерация `Service Ticket` и `User Ticket` (не поддерживается в [стартере](#стартер) отдельно от MJ)
- Возможность выключить tvm на отдельных ручках

## Настройка TVM для сервиса
Настройка tvm сервиса происходит в `service.yaml` в разделе [tvm](../how_it_works/configuration/service_yaml.md#tvm-self).
Можно указать:
* _id_ - свой tvm id
* _sources_ - список tvm id сервисов, которым разрешен доступ к вашему сервису.
* _destinations_ - список tvm id сервисов, куда этот сервис планирует ходить. Для сервисов, клиенты к которым были сгенерированы в разделе [clients](../how_it_works/configuration/service_yaml.md#clients), tvm id здесь указывать не обязательно, они подхватятся из настроек клиентов.
* _serverTvmDisabled_ - отключение tvm на серверной части (контроллерах) сервиса. Бывает полезно для отладки в среде `local`
* _clientsTvmDisabled_ - отключение tvm на сгенерированных клиентах сервиса. Бывает полезно для отладки в среде `local`

Так же можно отключить tvm или включить проверку User Ticket для конкретной ручки в [api.yaml](../how_it_works/configuration/api_yaml.md#про-tvm)
* _disableSecurity_ - отключение проверки tvm
* _checkUserTicket_ - включение проверки наличия user ticket

Значения можно переопределять для разных сред, как описано [тут](../how_it_works/configuration/environment.md).

Пример service.yaml:
```yaml
tvm:
  id: 123
  sources:
    - 345
    - 657
  destinations:
    - 2028530
    - 224
  env:
    local:
      serverTvmDisabled: true
      clientsTvmDisabled: true
    testing:
      id: 234
    production:
      id: 345
```

Пример api.yaml:
```yaml
paths:
    /helloWorld:
        get:
            tags:
                - helloWorld
            x-settings:
                checkUserTicket: true
                env:
                    testing:
                        disableSecurity: true
    responses: #...
```

## Отключение TVM у негенерируемых ручек
Если у вас имеются ручки, которые не сгенерированы с помощью MJ и хочется убрать из них TVM, то необходимо реализовать [интерфейс](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/mj/v1/mj-security/src/main/java/configurer/FrameworkWebSecurityConfigurer.java), добавив в метод `configure` строчку
`web.ignoring(<path>)`, где в `<path>` указать необходимые ручки.

## Настройка TVM для клиентов
Для [кодогенерируемых клиентов](clients.md) так же есть поддержка TVM, которая включается при указании собственного tvm id в [service.yaml](../how_it_works/configuration/service_yaml.md#tvm-self).
Если сервис, к которому генерируется клиент, написан на MJ, то настройки TVM подхватятся автоматически.

Если сервис написан не на MJ, то есть возможность указания tvm id вручную. TVM проверку для Service Ticket или для User Ticket можно отключить. Подробнее [здесь](clients.md#Создание-клиента-к-любому-сервису).

## Стартер
Предназаначен для быстрого подключения **TVM** в любой проект на **Spring Boot**

### Уровень: новичок
_У вас есть небольшой проект на Spring Boot и хочется включить проверку Service Ticket'ов._

1. Добавить зависимость в свой ya.make:
   ```
   PEERDIR(
       market/infra/java-application/spring-boot-starters/tvm-spring-boot-starter
   )
   ```
2. Задать в properties следующие параметры:
   ```
   tvm.id=111
   tvm.enableFilterAutoRegistration=true
   tvm.sources[0].id=222
   tvm.sources[1].id=333
   tvm.destinations[0].id=444
   ```
   
   - _id_ - tvm id собственного сервиса
   - _enableFilterAutoRegistration_ - Spring автоматически зарегистрирует `ServiceTicketFilter` и `UserTicketFilter`. Для этого не надо создавать Security конфигурацию. Есть недостаток: если у вас все таки есть Security конфигурация, то в WebSecurity метод ignoring не будет полностью отключать защиту ручки - фильтры все равно будут действовать. Если это не устраивает, то решение в следующем разделе.
   - _sources_ - tvm id сервисов, которым разрешен доступ к вашему сервису
   - _destinations_ - tvm id сервисов, в которые ваш сервис собирается "ходить"

### Уровень: средний
_У вас уже есть проект с Security конфигурацией, в которую нужно аккуратно внедриться._

1. Добавить зависимость в свой ya.make:
   ```
   PEERDIR(
       market/infra/java-application/spring-boot-starters/tvm-spring-boot-starter
   )
   ```
2. Задать в properties следующие параметры:
   ```
   tvm.id=111
   tvm.sources[0].id=222
   tvm.sources[1].id=333
   tvm.destinations[0].id=444
   ```
3. Добавить в свою Security конфигурацию необходимые фильтры
   ```java
   @Configuration
   public class WebSecurityConfiguration implements WebSecurityConfigurer {

       @Autowired
       private ServiceTicketFilter serviceTicketFilter;
       @Autowired
       private UserTicketFilter userTicketFilter;

       @Override
       public void configure(final HttpSecurity http) throws Exception {
           http
               ....
               .addFilterBefore(userTicketFilter, BasicAuthenticationFilter.class)
               .addFilterBefore(serviceTicketFilter, BasicAuthenticationFilter.class)
               ....
       }
   }
   ```
4. Если нужно проверять User Ticket'ы, то отнаследоваться от TvmConfigurerAdapter и переопределить метод getUserTicketProtectedPaths(), а также задать проперти `tvm.blackboxEnv` с указанием среды blackbox, в которой нужно проверять User Ticket. [Возможные варианты значений](https://a.yandex-team.ru/arc_vcs/library/java/tvmauth/src/main/java/ru/yandex/passport/tvmauth/BlackboxEnv.java).

   ```java
   @Configuration
   public class UserTicketsConfigurer extends TvmConfigurerAdapter {

       @Override
       public Set<AntPathRequestMatcher> getUserTicketProtectedPaths() {
           return Set.of(new AntPathRequestMatcher("/api/**"));
       }
   }
   ```

### Уровень: продвинутый
_Если хочется еще большей гибкости_

1. Дополнительные поля
   ```
   tvm.serverTvmDisabled=true
   tvm.useDefaultLocalTvmId=true
   tvm.accessToTestingFromLocalDisabled=true
   tvm.id=111
   tvm.secret="dsffsdf"
   tvm.sources[0].id=222
   tvm.sources[1].id=333
   tvm.destinations[0].id=444
   ```

   - _serverTvmDisabled_ - отключить проверку тикетов (удобно для отладки в локальной среде, например). По умолчанию проверка включена.
   - _useDefaultLocalTvmId_ - в локальной среде использовать tvm id [этого сервиса](https://abc.yandex-team.ru/services/market-local-environment-service/), чтобы была возможность ходить в тестинг других сервисов, разрешающих доступ (К таковым относятся сервисы, написанные на MJ). Параметр будет только если у вас явно не задан `id`. По умолчанию отключено.
   - _accessToTestingFromLocalDisabled_ - в противоположность предыдущему свойству, отключить доступ к вашему тестингу из локальной среды. По умолчанию доступ есть.

2. Если нужно реализовать какую-то логику для задания `sources` или `destinations`, то можно отнаследоваться от уже известного `TvmConfigurerAdapter` и переопределить следующие методы:
   ```java
   @Configuration
   public class MoreSourcesAndDestinationsConfigurer extends TvmConfigurerAdapter {

       @Override
       public Set<TvmIdRef> getSources() {
           if (!Environments.IS_TESTING) {
               return Set.of(new TvmIdRef(555));
           }
           return Set.of(new TvmIdRef(666));
       }

       @Override
       public Set<TvmIdRef> getDestinations() {
           if (!Environments.IS_TESTING) {
               return Set.of(new TvmIdRef(777));
           }
           return Set.of(new TvmIdRef(888));
       }
   }
   ```

3. Добавление генерации тикетов в клиенты
   
   {% note info %}

   В Market Java Framework данная функциональность уже реализована. Если вы бы хотели пользоваться фреймворком, но вам не хватает какой-либо TVM фичи, то можно написать нам в [чат поддержки](https://t.me/joinchat/RImGNXqbohFkOTg6).

   {% endnote %}

   3.1. Инжектим в ваш клиент бин TvmClient, генерим Service Ticket и добавляем его в заголовок запроса (пример концептуальный, не стоит использовать его в таком виде):
   ```java
   public class AbstractClient {
   
       private static final int DST_TVM_ID = 111;
       
       @Autowired
       private AsyncHttpClient client;
       
       @Autowired
       private TvmClient tvmClient;
       
       public ListenableFuture<Response> executeRequest(RequestBuilder requestBuilder) {
           final Request request = requestBuilder
               .addHeader("X-Ya-Service-Ticket", tvmClient.getServiceTicketFor(DST_TVM_ID))
               .build();
           return client.executeRequest(request);
       }
   }
   ```
   4.2. Если необходимо генерить User Ticket, то нужно добавить дополнительную зависимость:
   ```
   market/infra/java-application/spring-boot-starters/blackbox-spring-boot-starter
   ```

   Далее заинжектить Blackbox2, сгенерить User Ticket и добавить его в заголовок запроса `X-Ya-User-Ticket`.
