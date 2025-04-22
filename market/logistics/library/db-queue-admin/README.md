# Библиотека для подключения админки DBQueue в интерфейс LMS

Реализации для разных версий DBQueue находятся во dbqueue-admin-impl. Например, `market/logistics/library/db-queue-admin-impl/v8/`
нужно подключать, если у вас DBQueue версии 8.
При правильном подключении в интерфейсе компонента в LMS активируется пункт "DB Queue" в левом меню.

## Как подключить
1. В компонент добавить зависимость `market/logistics/library/db-queue-admin-impl/v8`
2. В LMS-плагине переопределить метод
    ```
   @Override
   public boolean isDbQueueAdminEnabled() {
       return true;
   }
    ```
3. Добавить пользователю роль `DbQueueProxyController.AUTHORITY_ROLE_DB_QUEUE` в плагине. Пример:
    ```
       @Override
    public Set<Role> getRoles() {
        Role viewer = new Role(
            VIEWER_CODE,
            "Доступ на просмотр",
            AUTHORITY_ROLE_TRANSPORTATIONS,
   
            //// Вот так
            DbQueueProxyController.AUTHORITY_ROLE_DB_QUEUE
            //// 
        );
        ..........
        return Set.of(viewer, admin);
    }
   ```
4. Добавить аннотацию `@EnableDbQueueAdmin` к spring-конфигурации, либо явно сделать `@Import(DbQueueAdminConfiguration.class)`
5. Объявить бин типа `ru.yandex.market.logistics.dbqueue.domain.QueueMetaProvider`, который предоставит информацию о существующих очередях
6. Для подключения доп. функционала истории нужно переопределить бин
    ```
    @Bean
    @Primary
    public DbQueueTaskLogDao taskExtDao(DataSource dataSource) {
        return new DbQueueTaskLogDaoImpl(
            dbQueueProperties.getTableNameExt(),
            new NamedParameterJdbcTemplate(dataSource)
        );
    }
   ```
   После этого на страничке каждой dbqueue задачи будет показаны все её запуски. Для его работы нужна кастомная таблица, 
   куда пишется лог dbqueue, request_id запусков и т.д.
