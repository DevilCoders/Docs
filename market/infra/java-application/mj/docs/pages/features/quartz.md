# Модуль Quartz

## Особенности
* В основе лежит `spring-boot-starter-quartz`
* Интегрированы все наработки из [tms-core-quartz2](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2)
* Большинство настроек можно произвести заданием параметров через [service.yaml](../how_it_works/configuration/service_yaml.md). В одном месте можно задать все необходимые [настройки для каждой среды](../how_it_works/configuration/environment.md).
* Генерируются заглушки для тестов и шаблоны создания простых задач
  Эту функцию можно [отключить](generation_settings.md).

## Конфигурация
### Возможности из spring-boot-starter-quartz
*  В service.yaml можно настроить проперти перечисленые [здесь](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.core.spring.quartz.auto-startup), заменив префикс `spring.quartz` на раздел `modules.quartz`. Пример:
  ```yaml
  modules:
    quartz:
      schedulerName: customSchedulerName
      autoStartup: false
      startupDelay: 5
  ```
* [Проперти кварца](http://www.quartz-scheduler.org/documentation/2.3.1-SNAPSHOT/configuration.html) можно задавать в разделе `modules.quartz.properties.*`
  Пример:
  ```yaml
  modules:
  quartz:
    properties:
      org.quarz:
        scheduler:
          instanceName: MyScheduler
          instanceId: someId
          jmx:
            objectName: customName
        threadPool:
          threadPriority: MIN_PRIORITY
          threadCount: 20
  ```
* Можно создавать сущности кварца и они автоматически подхватятся. Допустимо создавать следующие сущности:
  - `org.quartz.JobDetail`
  - `org.quartz.Calendar`
  - `org.quartz.Trigger`
  - `org.quartz.SchedulerListener`
  - `org.quartz.JobListener`
  - `org.quartz.spi.JobFactory` (По умолчанию используется [AutowiringSpringBeanJobFactory](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/AutowiringSpringBeanJobFactory.java))
* По умолчанию для кварца используется основной `Datasource`, `TransactionManager` и `JdbcTemplate`. Чтобы использовать для кварца отдельный `Datasource`, необходимо реализовать [TmsDataSourceConfig](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/spring/config/TmsDataSourceConfig.java).
* Чтобы донастроить `SchedulerFactoryBean`, можно реализовать `org.springframework.boot.autoconfigure.quartz.SchedulerFactoryBeanCustomizer`. Но при добавлении **стоит еще раз задуматься**, потому что скорее всего проблему можно решить с помощью предыдущих пунктов.
* Для ускорения выполнения задач можно использовать партиционирование задач (механизм разбивки задачи по партициям).
  Пример:
  ```java
  @Configuration
  public class TmsJobsConfig {
      @Bean
      @CronTrigger (cronExpression = "0 */1 * * * ? *")
      @PartitionedTask ( size = 10 )
      public PartitionExecutor notificationEvictionTmsJob() {
          return new NotificationEvictionJob();
      }
  }
  
  public class NotificationEvictionJob implements PartitionExecutor {
      @Override
      public void doJob(JobExecutionContext context, int partition) {
          // здесь логика обработки данных в зависимости от partition
      }
  }
  ```

  Аннотация `PartitionedTask` автоматически размножит бин `notificationEvictionTmsJob` на 10 экземпляров + создаст для каждого из них свой триггер и мониторинг.
  (Имена будут сформированы автоматически путём добавления "_" и номера партиции, начиная с нулевой)
  В `CronTrigger.cronExpression` и `PartitionedTask.size` можно использовать строковые выражения (то, что можно писать в аннотации `Value` у `Spring`), чтобы можно было гибко настроить из внешних файлов конфигураций.

### Возможности из tms-core-quartz2
- Настройки указываются в разделе `modules.quartz.extensions`
- Уже созданы следующие сервисы (_при необходимости можно создать свою версию сервиса, тогда дефолтная версия создаваться не будет_):

  - [JobService](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/service/JobService.java) 
  - [JobHistoryService](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/logging/JobHistoryService.java). Можно конфигурировать через проперти в `modules.quartz.jobHistory.*`. Доступные проперти и их дефолтные значения: 
    ```yaml
    modules:
      quartz:
        extensions:
          jobHistory:
            statusMaxLength: 200
            logTableName: qrtz_log
            selectLogTableName: null
            saveFullLogs: false
            attachTraceId: false
            jobStatusesToSkip: <пустой лист>
            skipEmptyJobStatuses: false
            traceModule: null
            daysToKeepLogs: 30
    ```
  - [JobLogAnalysisService](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/service/JobLogAnalysisService.java)
  - [JobMonitoringResultCache](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/logging/JobMonitoringResultCache.java)
  - [TmsMonitoringService](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/service/TmsMonitoringService.java). Можно конфигурировать в `modules.quartz.extensions.jobMonitoring.*`. Доступные проперти и их дефолтные значения:
    ```yaml
    modules:
      quartz:
        extensions:
          jobMonitoring:
            failsToCrit: 1
            failsToWarn: 1
            responsibleTeam: 
            maxDelayTimeMillis: -1
            maxExecutionTimeMillis: -1
            onNotStartedYetStatus: CRIT
            onNeverBeenFinishedYetStatus: CRIT
            skipHealthCheck: false
            skipHealthCheckReason:
            tmsResultCacheExpire: 60
    ```
  - [QrtzLogTableCleaner](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/util/QrtzLogTableCleaner.java)

* При запуске приложения по умолчанию запускается удаление неиспользуемых триггеров. Отключить можно с помощью настройки:
  ```yaml
  modules:
    quartz:
      extensioins:
        cleanOnStartup: false
  ```
  Также можно задать свой `GroupMatcher` для изменения набора подчищаемых джоб. При этом надо использовать `Qualifier` для бина: 
  ```java
    @Qualifier(RemoveUnusedTriggersSchedulerListener.JOBS_TO_REMOVE_QUALIFIER)
  ```
  По умолчанию используется `GroupMatcher.anyJobGroup()`
* При завершении работы приложения незавершенные джобы обрабатываются в [JobHistoryService::executionException](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/logging/DbJobHistoryService.java#L255).
* Поддерживается аннотация [@CronTrigger](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2#shag-4-obuyavlenie-tms-zadach) и [@MonitoringConfig](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2#annotaciya-monitoringconfig). Можно сконфигурировать в разделе `modules.quartz.extensions.annotatedTrigger.*` По умолчанию крон-выражения отключены для _Memory_ режима и включены для _Jdbc_ режима. Чтобы вручную изменить эту логику, можно использовать `modules.quartz.extensions.annotatedTrigger.cronEnabled=<true/false>`.
  Доступные проперти и их дефолтные значения:
  ```yaml
  modules:
    quartz:
      extensions:
        annotatedTrigger:
          cronEnabled: null
          misfireInstruction: MISFIRE_INSTRUCTION_DO_NOTHING
          requestRecovery: false
  ```
* Добавлена конфигурация [TmsCommandsConfig](https://a.yandex-team.ru/arc_vcs/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/spring/config/TmsCommandsConfig.java) вместе с [CommandExecutor](https://a.yandex-team.ru/arc_vcs/market/jlibrary/common-util/src/main/java/ru/yandex/common/util/terminal/CommandExecutor.java) и [RemoteControlServer](https://a.yandex-team.ru/arc_vcs/market/jlibrary/common-util/src/main/java/ru/yandex/common/util/terminal/RemoteControlServer.java). **По умолчанию выключена**. Для активации добавить
  ```yaml
  modules:
    quartz:
      extensions:
        tmsCommands:
          enabled: true
  ```
  Можно создать свои версии `CommandExecutor` или `RemoteControlServer`, тем самым переопределив дефолтные.
  Доступные проперти и их дефолтные значения
  ```yaml
  modules:
    quartz:
      extensions:
        tmsCommands:
          enabled: false
          port: 0
          terminalName: unknown-terminal
          noOpenFilesAcceptDelay:0
  ```


### Локальный запуск
По умолчанию _Quartz_ настроен для работы с базой данных (`modules.quartz.job-store-type=jdbc`). Чтобы все хранить в памяти, надо указать `modules.quartz.job-store-type=memory`.

#### Дефолтные настройки
**Все эти настройки можно переопределить заданием своих собственных значений.**

Memory
```yaml
modules:
  quartz:
    scheduler-name: qrtz2-scheduler
    waitForJobsToCompleteOnShutdown: true
    overwriteExistingJobs: true
```

Jdbc
Все то же, что и для _Memory_ режима, а также:
```yaml
modules:
  quartz:
    properties:
        org.quartz:
          jobStore:
            driverDelegateClass: org.quartz.impl.jdbcjobstore.StdJDBCDelegate
            selectWithLockSQL: SELECT * FROM {0}LOCKS UPDLOCK WHERE LOCK_NAME = ? FOR UPDATE
            isClustered: true
          scheduler:
            instanceId: AUTO
            jmx.export: true
          threadPool.class: org.quartz.simpl.SimpleThreadPool
```

### Пример конфигурации
Таким образом, с учетом дефолтных настроек финальная конфигурация может выглядеть примерно так:
```yaml
modules:
  quartz:
    env:
      local:
        jobStoreType: MEMORY
```

* В локальном окружении (`-Denvironment=local`) будет использоваться _in-memory_ конфигурация кварца. `Datasource` в данном случае не нужен.
* В `production`, `testing` и других средах (_т.к. не задали отдельных конфигураций_) будут использоваться [дефолтные настройки](#дефолтные-настройки): для доступа к базе будет использоваться основной `Datasource` из контекста спринга и т.д.

## Тестирование
  Для простоты тестирования можно свои тесты наследовать от `ru.yandex.market.javaframework.quartz.test.AbstractQuartzTest`. С помощью `@ContextConfiguration` можно передавать свои бизнесовые компоненты.
  
```java
@ContextConfiguration(classes = TmsTasks.class)
public class TmsTaskTest extends AbstractQuartzTest {
    @Autowired
    public NamedParameterJdbcTemplate jdbcTemplate;

    @Autowired
    @Qualifier("tmsLogsCleanupExecutor")
    public Executor tmsLogsCleanupExecutor;

    @Test
    public void testTask() {
      tmsLogsCleanupExecutor.doJob(mockContext());
      jdbcTemplate.query("select * from qrtz_job_details", (rs) -> {
        System.out.println(rs.getString("JOB_NAME"));
      });
    }
}
```

## Стартер
Стартер предназаначен для быстрого подключения **Quartz** в любой проект на **Spring Boot**

### Установка
Добавить в `ya.make` зависимость:
```
market/infra/java-application/spring-boot-starters/quartz-spring-boot-starter
```

### Конфигурирование
- Большинство настроек можно произвести заданием параметров через properties-файлы. Доступные проперти перечислены [здесь](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.core.spring.quartz.auto-startup).
- [Проперти кварца](http://www.quartz-scheduler.org/documentation/2.3.1-SNAPSHOT/configuration.html) можно задавать с префиксом spring.quartz.properties.*
- Настройки `modules.quartz.extensions` [отсюда](#--tms-core-quartz2) можно указать в пропертях, заменив `modules.quartz.extensions` на `mj.quartz`. Доступные проперти и их дефолтные значения:
  ```
  mj.quartz.jobHistory.statusMaxLength=200
  mj.quartz.jobHistory.logTableName=qrtz_log
  mj.quartz.jobHistory.selectLogTableName=null
  mj.quartz.jobHistory.saveFullLogs=false
  mj.quartz.jobHistory.attachTraceId=false
  mj.quartz.jobHistory.jobStatusesToSkip=<пустой лист>
  mj.quartz.jobHistory.skipEmptyJobStatuses=false
  mj.quartz.jobHistory.traceModule=null
  mj.quartz.jobHistory.daysToKeepLogs=30
  
  mj.quartz.jobMonitoring.failsToCrit=1
  mj.quartz.jobMonitoring.failsToWarn=1
  mj.quartz.jobMonitoring.responsibleTeam=
  mj.quartz.jobMonitoring.maxDelayTimeMillis=-1
  mj.quartz.jobMonitoring.maxExecutionTimeMillis=-1
  mj.quartz.jobMonitoring.onNotStartedYetStatus=CRIT
  mj.quartz.jobMonitoring.onNeverBeenFinishedYetStatus=CRIT
  mj.quartz.jobMonitoring.skipHealthCheck=false
  mj.quartz.jobMonitoring.skipHealthCheckReason=
  mj.quartz.jobMonitoring.tmsResultCacheExpire=60
  
  mj.quartz.cleanOnStartup=true
  
  mj.quartz.annotatedTrigger.cronEnabled=null
  mj.quartz.annotatedTrigger.misfireInstruction=MISFIRE_INSTRUCTION_DO_NOTHING
  mj.quartz.annotatedTrigger.requestRecovery=false
  
  mj.quartz.annotatedTrigger.cronEnabled=null
  mj.quartz.annotatedTrigger.misfireInstruction=MISFIRE_INSTRUCTION_DO_NOTHING
  mj.quartz.annotatedTrigger.requestRecovery=false
  ```
- Для базы данных [для локального запуска](#локальный-запуск) используется пропертя `spring.quartz.job-store-type` (доступные значения: `jdbc`, `memory`). Дефолтные настройки:
  
  _Memory_
  ```
  spring.quartz.scheduler-name=qrtz2-scheduler
  spring.quartz.waitForJobsToCompleteOnShutdown=true
  spring.quartz.overwriteExistingJobs=true
  ```
  _JDBC_ все то же, что и для Memory режима, а также:
  ```
  spring.quartz.properties.org.quartz.jobStore.driverDelegateClass=org.quartz.impl.jdbcjobstore.StdJDBCDelegate
  spring.quartz.properties.org.quartz.jobStore.selectWithLockSQL=SELECT * FROM {0}LOCKS UPDLOCK WHERE LOCK_NAME = ? FOR UPDATE
  spring.quartz.properties.org.quartz.jobStore.isClustered=true
  spring.quartz.properties.org.quartz.scheduler.instanceId=AUTO
  spring.quartz.properties.org.quartz.threadPool.class=org.quartz.simpl.SimpleThreadPool
  spring.quartz.properties.org.quartz.scheduler.jmx.export=true
  ```

## Куда присылать фидбек
На данный момент стартер имеет базовый функционал и подготовлен для дальнейшего расширения. Предложения по добавлению новых функций приветствуются - приходите к нам в [чат](https://t.me/joinchat/RImGNXqbohFkOTg6).
