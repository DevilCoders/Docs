deepmind-tracker-approver
----
Небольшая либа, предназначенная на согласование чего либо через трекер. Примеры:

- Перевод ssku в статус с согласованием ассортиментного комитета
- Привязка катмена к категории с согласованием администратора системы

Подробное описания на вики: https://wiki.yandex-team.ru/market/deepmind/trebovanija/avtomatizacija-assortimentnogo-komiteta/dvizhok-po-vzaimodejjstviju-s-trekerom/

Особенности:
- в одном тикете может согласовывать данные по одному или нескольким объектам
- хранит состояние согласования в БД
- описывает сценарии взаимодействия с трекером в виде джава кода
- не ограничивает в тексте создаваемых тикетов. Текст разработчик должен описать самтоятельно
- ведет историю изменений

Что либа не делает:
- не мигрирует внутреннюю базу данных. Миграцией должен заниматься liquibase основного сервиса

Использование
----
1. Добавьте в ваш проект `PEERDIR(market/mbo/mbo-category/deepmind-tracker-approver)`
2. Добавьте в миграции:
   ```xml
    <property name="tracker_approver.schema" value="<ВАША СХЕМА>"/>

    <include file="classpath:/migrations/tracker_approver/tracker_approver.liquibase.xml"/>
   ```
3. При создании DataSource-а нужно завернуть его в `InterceptingDataSource` + `DelegatingJdbcInterceptorSupplier` - это та точка, в которой для DML запросов будут инициализироваться данные с текущим запросом/пользователем.
    ```java
    @Bean
    public DelegatingJdbcInterceptorSupplier delegatingJdbcInterceptorSupplier() {
        return new DelegatingJdbcInterceptorSupplier();
    }

    @Bean
    public DataSource dataSource() {
        return new InterceptingDataSource<>(yourInternalDataSource(), delegatingJdbcInterceptorSupplier());
    }
    ```
1. Создать конфиг для поставщика контекста.
   ```java
   public class HistoryContextSetterConfig {
       @Value("${tracker_approver.schema}")
       private String schema;

       @Bean
       public HistoryContextSetter historyContextSetter(JdbcTemplate jdbcTemplate) {
           return new HistoryContextSetter(schema, jdbcTemplate);
       }

       @Bean
       public HistoryContextSupplier historyContextSupplierService() {
           return new HistoryContextSupplier() {
               public HistoryContext get() {
                   return new HistoryContext(
                        getCurrentUserLoginOrDefault(null),
                        Thread.currentThread().getName());
               }

               private static String getCurrentUserLoginOrDefault(String defaultLogin) {
                   Authentication authentication = SecurityContextHolder.getContext().getAuthentication();
                   return authentication != null ? authentication.getName() : defaultLogin;
               }
           };
       }

       @PostConstruct
       public void setupListener() {
           delegatingJdbcInterceptorSupplier().setSupplier(
               () -> new DbListenerForHistoryContext(
                   historyContextSetter(),
                   historyContextSupplierService()));
       }
   }
   ```
TODO описать простой пример и roadmap развития
