## Описание

### Что это и для чего

Spring конфигурация, позволяющая выполнять определенные quartz джобы на мастер-инстансах.

### Мастер-инстанс

Инстанс является "мастром", если его ДЦ нет в списке реплик базы данных из таблицы `pg_replication_slots`.
За это отвечает бин `DatabaseMasterEnvironmentPredicate`.

Кроме этого, можно дополнительно указать, в каких ДЦ (vla, iva, sas...) инстансы считаются "мастером" по-умолчанию:

`host-aware-quartz-config.considered-master-data-centers=vla, iva, sas`

Это свойство может пригодиться, например, если в ДЦ, в котором находится мастер-БД, нет инстансов приложения
(в данном случае будет считаться, что мастера нет нигде и джоба выполняться не будет).

### Кеширование

По-умолчанию запросы в `pg_replication_slots` кешируются (1 минута). Кеширование настраивается следующими свойствами:

`host-aware-quartz-config.cache-enabled`  
`host-aware-quartz-config.cache-expires-after-write`

Все свойства хранятся в классе `HostContextAwareConfigurationProperties`.

## Подключение

### Конфигурация

Конфигурация `HostContextAwareConfiguration` подключается стандартным образом, за исключением одного момента:  
Конфигурация, которая настраивает quartz (не джобы, а именно сам quartz) в вашем приложении, должна зависеть
от `HostContextAwareConfiguration`.

Сделать это можно, воспользовавшись аннотацией `@DependsOnHostContextAwareConfiguration`.

Пример подключения:

```java
@Configuration
@Import({
    HostContextAwareConfiguration.class,
})
@DependsOnHostContextAwareConfiguration
public class QuartzConfiguration
```

### Delegate

Помимо конфигурации, в свойствах quartz для вашего приложения необходима следующая строка:

`org.quartz.jobStore.driverDelegateClass=ru.yandex.market.logistics.config.quartz.hostcontextaware.HostContextAwareSQLDelegate`

## Джоба для мастера

По-умолчанию все джобы будут продолжать выполняться в обычном режиме на всех инстансах.
Чтобы джоба выполнялась только на мастере, в `jobMapData` нужно добавить ключ
**EXECUTE_ON_MASTER** со значением **true**:

```java
@CronTrigger(
    cronExpression = "* * * * * *",
    description = "Описание джобы",
    jobData = @JobDataEntry(key = HostContextAwareSQLDelegate.KEY_EXECUTE_ON_MASTER, value = "true")
)
```
