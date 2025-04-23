## Описание
Реализация TMS фреймворка для quartz версии 2+ и spring 4+

# Публикация
Публикация либы производится после коммита в мастер автоматически через релизную машину:
https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/tms-core-quartz2-java-library

## Для пользователей библиотеки

### Включение TMS в модуле

#### Шаг 0 - подготовка таблиц в базе данных
Для работы в кластере библиотека quartz использует базу данных для хранение задач и триггеров, а так же 
синхронизации их выполнения. Для этого она требует, чтобы в базе данных имелся набор таблиц. Скрипты для 
создания таблиц для разных типов баз данных можно найти здесь - 
https://github.com/elventear/quartz-scheduler/tree/master/distribution/src/main/assembly/root/docs/dbTables

При необходимости, можно выбрать произвольный префикс таблиц вместо ```QRTZ_``` и указать его в настройках.

Кроме этих таблиц, TMS также требует наличия таблицы для записи логов выполнения задач (синтаксис Oracle):
```
CREATE TABLE QRTZ_LOG (
  ID NUMBER GENERATED ALWAYS as IDENTITY(START with 1 INCREMENT by 1),
  JOB_NAME VARCHAR2(80 CHAR) NOT NULL,
  JOB_GROUP VARCHAR2(80 CHAR) NOT NULL,
  TRIGGER_FIRE_TIME TIMESTAMP NOT NULL,
  JOB_FINISHED_TIME TIMESTAMP,
  JOB_STATUS VARCHAR2(200 CHAR),
  HOST_NAME VARCHAR2(80 CHAR) NOT NULL
);

CREATE INDEX i_tft_jnm_hnm__premod_qlog
  ON qrtz_log(TRIGGER_FIRE_TIME, JOB_NAME, HOST_NAME);
  
CREATE INDEX i_id__premod_qlog
  ON premod_qrtz_log(ID);
```

#### Шаг 1 - подключение необходимых конфигураций к Spring контексту

Библиотека предоставляет подготовленный набор spring java конфигов, которые необходимо включить в существующую 
spring конфигурацию. Существующие конфигурации:
* ```ru.yandex.market.tms.quartz2.spring.config.DatabaseSchedulerFactoryConfig```
* ```ru.yandex.market.tms.quartz2.spring.config.RAMSchedulerFactoryConfig```
* ```ru.yandex.market.tms.quartz2.spring.config.TmsCommandsConfig``` - подключение данной конфигурации требует наличия
в контексте зарегистрированного бина с типом ```ru.yandex.common.util.terminal.CommandExecutor```. 
При регистрации данного бина в контексте становится доступна telnet консоль для управления приложением и в т. ч. 
TMS задачами. По умолчанию консоль не не содержит даже базовых команд (```exit``` и ```help```), поэтому для 
корректной работы необходимо их также зарегистрировать.

Описание преднзначения каждой из них можно найти в javadoc.

Конфигурации можно подключить следующим образом:
```
@Configuration
@Import({
    DatabaseSchedulerFactoryConfig.class, RAMSchedulerFactoryConfig.class,
    TmsCommandsConfig.class,
})
public class AppConfig {

}
```
Если модуль использует только XML конфигурации, то эти конфигурации можно подключить как анонимные бины:
```
<beans ...>
...
    <context:annotation-config/>
    <bean class="ru.yandex.market.tms.quartz2.spring.config.DatabaseSchedulerFactoryConfig"/>
    <bean class="ru.yandex.market.tms.quartz2.spring.config.RAMSchedulerFactoryConfig"/>
    <bean class="ru.yandex.market.tms.quartz2.spring.config.TmsCommandsConfig"/>
...
</beans>
```

Кроме подключения конфигураций, необходимо в контексте зарегистрировать бин, реализующий интерфейс 
```ru.yandex.market.tms.quartz2.spring.config.TmsDataSourceConfig```. Методы этого бина будут использоваться quartz 
и TMS движком для целей shared блокировок, сохранения данных о выполнении задач и очистки логгов выполнения задач. 
Для этих целей рекомендуется выделить в пуле более 2 соединений.
Для исполнения запросов внутри задач использование бина не предполагается. Рекомендуется использование отдельного пула 
соединений с базой данных для инфраструктуры TMS, чтобы перегрузка основого пула приложения не приводила
к проблемам с шедулингом задач.

#### Шаг 2 - настройка библиотеки TMS

Библиотека TMS для корректной работы требует установки свойства ```market.tms-core-quartz2.qrtzLogTableName```. 
Это свойство задает имя таблицы (рекомендуется указание со схемой), которая будет использоваться для записи 
истории выполнения задач. 

Установка свойств может производиться любым способом (например через properties файлы приложения).

#### Шаг 3 - настройка библиотеки quartz

Настройки библиотеки quartz можно производить родными свойствами, описанными в документации - 
http://www.quartz-scheduler.org/documentation/quartz-2.x/configuration/

Для определения свойств можно:
* использовать файл ```classpath:quartz.properties``` 
* объявить в контексте бин с типом ```java.util.Properties``` и именем ```quartzProperties``` и 
наполнить его нужными проперти вручную

Нужно учитывать, что инициализация quartz шедулера производится при помощи 
```org.springframework.scheduling.quartz.SchedulerFactoryBean```, который проставляет некоторые проперти по умолчанию 
и сам конфигурирует ```DataSource```, которым будет пользоваться quartz, поэтому использование некоторых оригинальных 
свойств могут с ним конфликтовать.

Для установки в production и testing окружениях рекомендуются свойства:
* ```org.quartz.jobStore.tablePrefix``` - префикс таблиц, которые использует ```quartz```, по умолчанию ```QRTZ_```.
В данное проперти прдлагается явное указание схемы
* ```org.quartz.threadPool.threadCount``` - количество тредов в тред пуле для TMS задач, по умолчанию 10 (из 
```org.springframework.scheduling.quartz.SchedulerFactoryBean```)

Существует особенность настройки quartz для запуска на основе БД Postgre SQL - в свойствах ```quartzProperties```
необходимо указать свойство ```org.quartz.jobStore.driverDelegateClass``` со значением 
```org.quartz.impl.jdbcjobstore.PostgreSQLDelegate```

#### Шаг 4 - объявление TMS задач

TMS задачи могут объявляться непосредственно в java конфигурации компонента:
```
@Configuration
public class TmsTasksConfig {
    
    @Bean
    @CronTrigger(
       cronExpression = "0 * * * * ?",
       description = "Hello world executor"
    )
    public Executor helloWorldExecutor() {
        return (Executor) context -> {
                        System.out.println("Hello world from TMS");
                    };
    }
    
}
```
Кастомные имена бинов для экзекьюторов (заданные строкой внтури аннотации ```@Bean```) не поддерживаются, 
поэтому не следует их использовать при объявлении TMS задач.

При запуске JVM с аргументом ```-Dspring.profiles.active=development``` TMS задачи не запускаются автоматически. Для
запуска задачи следует использовать TMS консоль, которая подключается при помощи конфигурации 
```ru.yandex.market.tms.quartz2.spring.config.TmsCommandsConfig```

#### Дополнительная конфигурация

##### Очистка логов выполнения задач
Для очистки логов выполнения задач в конфигурации, подключаемой вместе с TMS framework, зарегистрирован бин с типом
```ru.yandex.market.tms.quartz2.util.QrtzLogTableCleaner``` и именем ```qrtzLogTableCleaner```.

Данный бин можно подключить к периодической очистке, например, добавив в существующую конфигурацию дополнительную
TMS задачу:
```
@Autowire
private QrtzLogTableCleaner qrtzLogTableCleaner;

...

@Bean
@CronTrigger(
        cronExpression = "0 0 4 1/1 * ?",
        description = "Задача очистки TMS логов в базе данных"
)
public Executor tmsLogsCleanupExecutor() {
    return (Executor) context -> qrtzLogTableCleaner.clean();
}
```

Для конфигурации времени хранения логов существует свойство ```market.tms-core-quartz2.daysToKeepLogs``` - 
количество дней, которое будут храниться логи выполнения задач в базе данных. Значение по умолчанию - 30 дней.

#### Мониторинг выполнения tms задач
В tms-core-quartz2 есть возможность получения результатов мониторингов по tms задачам компонента. 
Для этих целей нужно воспользоваться сервисом ```ru.yandex.market.tms.quartz2.service.TmsMonitoringService```, котоый 
будет доступен в spring контексте, если он настроен в соответствии с ранее описанными шагами. Метод 
```getTmsMonitoringResult(@Nullable String responsibleTeam)``` данного сервиса позволяет получить результат 
мониторингов по всем tms задачам компонента, назначенным на заданную команду (+ по задачам, которые ни на какие 
команды не заасайнены), либо по всем задачам компонента, если параметр не указан. Далее сервис можно 
использовать, например, в контроллере, возвращающем результаты мониторингов JUGGLER-у.

Также для работы с мониторингами можно воспользоваться утилитным классом 
```ru.yandex.market.tms.quartz2.util.TmsMonitoringResponseHelper```, который позволяет преобразовать результаты 
мониторингов задач в строковый формат, принимаемый JUGGLER-ом. 

##### Конфигурация мониторингов выполнения задач
tms-core-quartz2 позволяет задать некоторые настройки по работе с мониторингами. 

* **```failsToCritCount```** - количество последовательных запусков tms задач, завершившихся падением, после которого статус 
мониторинга становиться CRIT. Оцениваются только последние запуски задачи. Дефолтное значение 1.
* **```failsToWarnCount```** - количество последовательных запусков tms задач, завершившихся падением, после которого 
статус мониторинга становиться WARN. Оцениваются только последние запуски задачи. Дефолтное значение 1.
* **```responsibleTeam```** - команда, ответственная за данную tms задачу. По дефолту имеет пустое значение.
Статусы пот tms задачам, для которых команда не указана, будут возвращаться в мониторингах всех команд.
* **```maxDelayTimeMillis```** - максимальная задержка между окончанием предыдущего запуска tms задачи и началом нового в 
миллисекундах. Оценивается только для текущего состояния запуска.При превышении максимальной задержки запуска мониторинг
задачи загорается статусом CRIT. Дефолтное значение -1. Если параметр не сконфигурирован или имеет дефолтное значение, 
проверки длительности задержки не осуществляются.
* **```maxExecutionTimeMillis```** - максимальная длительность выполнения tms задачи в миллисекундах. Оценивается только для 
текущего состояния запуска. При превышении максимальной длительности выполнения мониторинг задачи загорается статусом 
CRIT. Дефолтное значение -1. Если параметр не сконфигурирован или имеет дефолтное значение, проверки длительности 
выполнения не осуществляются.
* **```jobStatusesToSkip```** - перечисленные через запятую шаблоны статусов завершения задач (для SQL-оператора LIKE).
Записи в логах запуска задач с такими статусами игнорируются мониторингом. 
Поддерживаются wildcard-ы ANSI SQL: ``_`` для одиночного символа и ``%`` для последовательности символов. 


Конфигурацию параметров можно осуществить 2-мя способами: через properties файл или с использованием аннотации на бине 
экзекьютора tms задачи. Если мониторинги не скофигурированы ни одним из этих способов, то настройки принимают 
дефолтные значения.

###### Properties файл
Properties файл позволяет задать параметры мониторингов сразу для всех tms задач компонента. Для этого нужно 
сконфигурировать следующие проперти:
```
market.tms-core-quartz2.failsToCrit=9
market.tms-core-quartz2.failsToWarn=6
market.tms-core-quartz2.responsibleTeam=DEFAULT_TEAM
market.tms-core-quartz2.maxDelayTimeMillis=123456000
market.tms-core-quartz2.maxExecutionTimeMillis=234567000
market.tms-core-quartz2.jobStatusesToSkip=some-status,%during service stopping
```

Переопределить их для отдельных tms задач можно в аннотации ```@MonitoringConfig```

###### Аннотация @MonitoringConfig
Аннотации ```@MonitoringConfig``` используется совместно с ```@CronTrigger``` 
во время объявления бина экзекьютора:
```
 @Bean
 @CronTrigger(
         cronExpression = "0 0 12 1 * ? 2042",
         description = "Executor with full monitoring config"
 )
 @MonitoringConfig(
         failsToCritCount = 5,
         failsToWarnCount = 3,
         responsibleTeam = "SHOPS",
         maxDelayTimeMillis = 3600000,
         maxExecutionTimeMillis = 600000,
         jobStatusesToSkip = {"some-status", "%during service stopping"}
 )
 public Executor executorWithFullConfig() {
     return context -> {
     };
 }
```
Параметры мониторингов, указанные в аннотации, переопределяют занчения, установленные в properties файле. 

Более подробное описание работы сервиса мониторинов можно найти в javadoc - ах 
```ru.yandex.market.tms.quartz2.service.TmsMonitoringService```, 
```ru.yandex.market.tms.quartz2.service.JobLogAnalysisService``` и 
```ru.yandex.market.tms.quartz2.util.TmsMonitoringResponseHelper```.

#### Подключение трассировки
Есть возможность создания контекста трассировки для каждой задачи с сохранением requestId в базу. 
Далее по этому requestId можно отследить ход исполнения задачки по логам или посмотреть в интерфейсе ЦУМа
https://tsum.yandex-team.ru/trace/

Настраивается такая возможность флажком `attachTraceId` в `DbJobHistoryService`, 
при этом подразумевается, что в вашей таблице для записи логов `QRTZ_LOG` есть колонка `TRACE_ID`.

## Сборка и тестирование
[ya.make](https://wiki.yandex-team.ru/yatool/make/)

## Собрать проект для idea
```ya ide idea --directory-based --group-modules=tree --no-local-executor --iml-in-project-root --with-content-root-modules --yt-store -lr <локальный путь>/mbo-category <папка спримаунченной акркадией>/market/mbo/mbo-category```
