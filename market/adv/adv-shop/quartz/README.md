## Библиотека для подключения quartz к проекту

1. ```ru.yandex.market.adv.config.QuartzTmsAutoconfiguration``` - автоконфигурация для подключения **quartz** к проекту.
2. ```ru.yandex.market.adv.config.QuartzApiAutoconfiguration``` - автоконфигурация для подключения api, через которое
   можно просматривать или менять задачи quartz.
3. ```ru.yandex.market.adv.config.QuartzTerminalAutoconfiguration``` - автоконфигурация для подключения terminal, через
   который можно просматривать или менять задачи quartz.

## Настройки

1. [Весь список](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/spring/config/TmsInitConfig.java)
2. ```market.tms-core-quartz2.tablePrefix``` - префикс quartz таблиц. По умолчанию **quartz_**.
3. ```market.tms-core-quartz2.driverDelegateClass``` - драйвер для сохранения результатов работы quartz job. По
   умолчанию **org.quartz.impl.jdbcjobstore.PostgreSQLDelegate**.
4. ```market.tms-core-quartz2.terminalPort``` - порт, через который можно подключиться по телнету к терминалу. По
   умолчанию функционал **выключен**. Для включения требуется прописать **значение доступного порта**.
5. ```market.tms-core-quartz2.api``` - включение api, через которое можно просматривать или менять задачи quartz. По
   умолчанию функционал **выключен**. Для включения требуется прописать **true**.

## Подключение quartz

1. Настроить БД согласно инструкции из ```market/adv/adv-shop/postgre/README.md```.
2. Добавить в ```resources/liquibase/db-changelog.xml``` следующую строчку:

```xml

<include file="quartz/changelog.xml" relativeToChangelogFile="true"/>
```

3. Добавить в ```resources/liquibase/quartz``` содержимое
   из [adv/content-manager](https://a.yandex-team.ru/arc_vcs/market/adv/content-manager/src/main/resources/liquibase/quartz)
   .
4. Прописать в настройках приложения ```market.tms-core-quartz2.qrtzLogTableName``` - название таблицы в которую будут
   писаться логи выполнения **job**, и ```market.tms-core-quartz2.traceModule``` - текущий модуль, используемый в
   трассировке. В качестве примера можно взять настройки
   из [adv/content-manager](https://a.yandex-team.ru/arc_vcs/market/adv/content-manager/src/main/properties.d/00_quartz.properties)
   или
   посмотреть [весь их список](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/tms-core-quartz2/tms-core-quartz2/src/main/java/ru/yandex/market/tms/quartz2/spring/config/TmsInitConfig.java)
   для кастомизации.
5. Описать задачу, которую требуется выполнять по расписанию. Например:

```java

@Configuration
public class QuartzTmsTasks {

    @Bean("tmsModerationTaskCreatedToSentExecutor")
    @CronTrigger(
        cronExpression = "0 */15 * * * ?",
        description = "Задача обработки задания на модерацию из CREATED в SENT"
    )
    public Executor tmsModerationTaskCreatedToSentExecutor(ModerationTaskCreatedToSentInteractor task) {
        return context -> task.process();
    }
}
```

6. В абстрактном классе для запуска тестов прописать:

```java

public abstract class AbstractContentManagerTest extends AbstractTest {

    protected JobExecutionContext mockContext() {
        return Mockito.mock(JobExecutionContext.class);
    }
}
```

7. Написать тест на **job**. Например:

```java

class ModerationTaskCreatedToSentYTInteractorTest extends AbstractContentManagerTest {
    @Autowired
    @Qualifier("tmsModerationTaskCreatedToSentExecutor")
    private Executor tmsModerationTaskCreatedToSentExecutor;

    @DisplayName("Проверка работоспособности job tmsModerationTaskCreatedToSentExecutor.")
    @DbUnitDataSet(
        before = "ModerationTaskCreatedToSentYTInteractor/csv/" +
            "tmsModerationTaskCreatedToSentExecutor_threeModerationTask_completeTwoTasksAndOneException.before.csv",
        after = "ModerationTaskCreatedToSentYTInteractor/csv/" +
            "tmsModerationTaskCreatedToSentExecutor_threeModerationTask_completeTwoTasksAndOneException.after.csv"
    )
    @Test
    void tmsModerationTaskCreatedToSentExecutor_threeModerationTask_completeTwoTasksAndOneException() {
        Assertions.assertThatThrownBy(() -> tmsModerationTaskCreatedToSentExecutor.doJob(mockContext()))
            .isInstanceOf(IllegalArgumentException.class)
            .hasMessage("Empty moderation content for task with id 443_4123_5732_BUSINESS");
    }
}
```

## Подключение api и terminal

### API

API, через которое можно просматривать или менять задачи quartz.

1. Прописать в настройках приложения ```market.tms-core-quartz2.api=true```.
2. [Документация по API](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/tms-core-quartz2/tms-web-quartz2/README.md)

### Terminal

Terminal, через который можно просматривать или менять задачи quartz.

1. Прописать в настройках приложения ```market.tms-core-quartz2.terminalPort=<значение доступного порта>```.
2. Подключиться к инстансу приложения по ssh и выполнить команду ```telnet localhost <порт из п.1>```.
3. Прописать ```help``` для получения списка доступных команд.

## Подключение мониторингов

1. Добавляются автоматически в виде ручки ```GET tms/jobs/status```.
2. Прописать в ```SecurityConfig``` ручку ```.antMatchers("/tms/jobs/status")``` для вытаскивания ее из под TVM.
3. [Настроить мониторинг в juggler](https://wiki.yandex-team.ru/advshop/backend-development/monitoring-settings/#nastrojjkajugglermonitoring)
4. Для кастомизации мониторинга job можно использовать аннотацию ```@MonitoringConfig```. Подробнее про ее использование
   можно почитать в javadoc.
