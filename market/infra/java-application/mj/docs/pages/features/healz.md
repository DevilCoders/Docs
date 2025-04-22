# Модуль Healz и Spring Actuator
## О модуле
Модуль Healz позволяет подключить преднастроенный Spring Actuator, а также собирать такие метрики, как:
- Тайминги по ручкам
- JVM метрики
- Метрики по ресурсам
- Метрики библиотек, которые публикуют свои метрики в Spring Boot Actuator, например Resilience4j, Hikari, JDBC и др.

{% cut "Неполный список сенсоров" %}

application_*
application_ready_time_seconds
application_started_time_seconds
disk_*
disk_free_bytes
disk_total_bytes
executor_*
executor_active_threads
executor_completed_tasks_total
executor_pool_*
executor_pool_core_threads
executor_pool_max_threads
executor_pool_size_threads
executor_queue_remaining_tasks
executor_queued_tasks
hikaricp_connections*
hikaricp_connections
hikaricp_connections_*
hikaricp_connections_acquire_seconds_*
hikaricp_connections_acquire_seconds_count
hikaricp_connections_acquire_seconds_max
hikaricp_connections_acquire_seconds_sum
hikaricp_connections_active
hikaricp_connections_creation_seconds_*
hikaricp_connections_creation_seconds_count
hikaricp_connections_creation_seconds_max
hikaricp_connections_creation_seconds_sum
hikaricp_connections_idle
hikaricp_connections_max
hikaricp_connections_min
hikaricp_connections_pending
hikaricp_connections_timeout_total
hikaricp_connections_usage_seconds_*
hikaricp_connections_usage_seconds_count
hikaricp_connections_usage_seconds_max
hikaricp_connections_usage_seconds_sum
http_server_requests_seconds*
http_server_requests_seconds
http_server_requests_seconds_*
http_server_requests_seconds_count
http_server_requests_seconds_max
http_server_requests_seconds_sum
jdbc_connections_*
jdbc_connections_active
jdbc_connections_idle
jdbc_connections_max
jdbc_connections_min
jetty_*
jetty_connections_*
jetty_connections_bytes_*
jetty_connections_bytes_in_bytes_*
jetty_connections_bytes_in_bytes_count
jetty_connections_bytes_in_bytes_max
jetty_connections_bytes_in_bytes_sum
jetty_connections_bytes_out_bytes_*
jetty_connections_bytes_out_bytes_count
jetty_connections_bytes_out_bytes_max
jetty_connections_bytes_out_bytes_sum
jetty_connections_current_connections
jetty_connections_max_connections
jetty_connections_messages_*
jetty_connections_messages_in_messages_total
jetty_connections_messages_out_messages_total
jetty_connections_request_seconds_*
jetty_connections_request_seconds_count
jetty_connections_request_seconds_max
jetty_connections_request_seconds_sum
jetty_threads_*
jetty_threads_busy
jetty_threads_config_*
jetty_threads_config_max
jetty_threads_config_min
jetty_threads_current
jetty_threads_idle
jetty_threads_jobs
jvm_*
jvm_buffer_*
jvm_buffer_count_buffers
jvm_buffer_memory_used_bytes
jvm_buffer_total_capacity_bytes
jvm_classes_*
jvm_classes_loaded_classes
jvm_classes_unloaded_classes_total
jvm_gc_*
jvm_gc_live_data_size_bytes
jvm_gc_max_data_size_bytes
jvm_gc_memory_*
jvm_gc_memory_allocated_bytes_total
jvm_gc_memory_promoted_bytes_total
jvm_gc_overhead_percent
jvm_gc_pause_seconds_*
jvm_gc_pause_seconds_count
jvm_gc_pause_seconds_max
jvm_gc_pause_seconds_sum
jvm_memory_*
jvm_memory_committed_bytes
jvm_memory_max_bytes
jvm_memory_usage_after_gc_percent
jvm_memory_used_bytes
jvm_threads_*
jvm_threads_daemon_threads
jvm_threads_live_threads
jvm_threads_peak_threads
jvm_threads_states_threads
log4j2_events_total
process_*
process_cpu_usage
process_files_*
process_files_max_files
process_files_open_files
process_start_time_seconds
process_uptime_seconds
resilience4j_ratelimiter_*
resilience4j_ratelimiter_available_permissions
resilience4j_ratelimiter_waiting_threads
system_*
system_cpu_*
system_cpu_count
system_cpu_usage
system_load_average_1m

{% endcut %}

Модуль подключается автоматически ко всем сервисам на последней версии MJ.

## Конфигурация Spring Actuator
Spring Actuator можно конфигурировать через [service.yaml](../how_it_works/configuration/service_yaml.md). Для этого нужно вписать проперти Spring Actuator в секцию modules.healz, например:
```yaml
modules:
  healz:
    management:
      security:
        enabled: false
      server:
        port: 7666
      endpoints:
        web:
          exposure:
            exclude: health
            include: '*'
      metrics:
        export:
          prometheus:
            enabled: true
      endpoint:
        beans:
          enabled: true
        metrics:
          enabled: true
        prometheus:
          enabled: true
        health:
          show-components: always
          show-details: always
          probes:
            enabled: true
```
Список пропертей по умолчанию можно посмотреть [здесь](https://a.yandex-team.ru/arcadia/market/infra/java-application/spring-boot-starters/healz-spring-boot-starter/src/main/resources/healz.properties).

Подробнее про Spring Actuator и его проперти можно прочитать в [документации](https://docs.spring.io/spring-boot/docs/current/actuator-api/htmlsingle/#overview).


## Про безопасность
Всю информацию от Spring Actuator можно получить по пути `/actuator`. Этот путь не защищен tvm.

По умолчанию по этому пути доступна информация [health](https://docs.spring.io/spring-boot/docs/current/actuator-api/htmlsingle/#health), [info](https://docs.spring.io/spring-boot/docs/current/actuator-api/htmlsingle/#info), [beans](https://docs.spring.io/spring-boot/docs/current/actuator-api/htmlsingle/#beans) и [prometheus](https://docs.spring.io/spring-boot/docs/current/actuator-api/htmlsingle/#prometheus).

При открытии через actuator других эндпоинтов (напр. [heapdump](https://docs.spring.io/spring-boot/docs/current/actuator-api/htmlsingle/#heapdump)), необходимо помнить про безопасность.
На порт actuator по умолчанию нельзя попасть через балансер, но все, кто имеет доступ до соответствующего порта (по умолчанию 7900), могут получить доступ к информации в actuator.

## Как получать метрики в Solomon
### 1. Положить в сервис конфиг для solomon agent

#### В случае Nanny
Положить [этот конфиг](https://sandbox.yandex-team.ru/resource/3183759283/view) в секцию files.
Туда можно попасть по ссылке ниже (не забудьте в url вставить id своего сервиса):
`https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_mj_service_vla/files`

Пример:
![](https://jing.yandex-team.ru/files/sid-hugo/Снимок%20экрана%202022-06-07%20в%2013.41.20.png)

#### В случае Deploy
Положить [этот конфиг](https://sandbox.yandex-team.ru/resource/3178440237/view) infra_box своего сервиса. 

- Переходим по ссылке ниже (не забудьте в url вставить id своего стейджа):
`https://deploy.yandex-team.ru/stages/testing_market_testapp-in-deploy-and-exp3/config`

- В правом верхнем углу нажимаем `edit`.
- Кликаем на свой deploy unit, справа кликаем на `Disk, volumes and resources`
- В секцию `layers` добавляем [этот конфиг](https://sandbox.yandex-team.ru/resource/3178440237/view)
![](https://jing.yandex-team.ru/files/sid-hugo/Снимок%20экрана%202022-06-07%20в%2013.49.10.png)
- Кликаем на левой панели на `infra_box`, заходим в `resources`
- В `layers` добавляем ресурс, который добавили на предыдущем шаге
![](https://jing.yandex-team.ru/files/sid-hugo/Снимок%20экрана%202022-06-07%20в%2013.51.59.png)


### 2. В своем проекте в Solomon создать сервис.

Для этого переходим по ссылке (не забудьте вставить id своего проекта):
   `https://solomon.yandex-team.ru/admin/projects/<your_project>/services/new`

Придумываем уникальный id, заполняем поля:
- **Monitoring model**: PULL
- **Port**: 7999
- **Url Path**: /storage/read?project=MJ&service=healz&pretty=true

Пример:
![](https://jing.yandex-team.ru/files/sid-hugo/1.png)
![](https://jing.yandex-team.ru/files/sid-hugo/Снимок%20экрана%202022-06-07%20в%2015.19.48.png)


### 3. Создаем кластеры для каждой среды (testing, production...)

Переходим по ссылке (не забудьте вставить id своего проекта):
`https://solomon.yandex-team.ru/admin/projects/<your_projet>/clusters/new`

Придумываем уникальный id, заполняем поля:
- **Label name**: значение метки cluster в метриках в solomon (обычно задают testing или stable)
- **Cluster hosts**: сюда добавить все хосты соответствующей среды

Пример:
![](https://jing.yandex-team.ru/files/sid-hugo/4.png)
![](https://jing.yandex-team.ru/files/sid-hugo/5.png)

### 4. Объединяем service и cluster в одну сущность: shard

Переходим по ссылке (не забудьте вставить id своего проекта):
`https://solomon.yandex-team.ru/admin/projects/<your_project>/shards/new`

Id пропускаем, в cluster и service выбираем сущности, которые создавали до этого.

### 5. Все готово

Теперь можно идти в Solomon и искать в своем проекте новые метрики.

## Как создавать свои метрики
Чтобы создать свои метрики, необходимо написать своего наследника класса [MeterBinder](https://github.com/micrometer-metrics/micrometer/blob/main/micrometer-core/src/main/java/io/micrometer/core/instrument/binder/MeterBinder.java) и добавить создание бина этого класса в свой @Configuration класс.

Примеры можно посмотреть [здесь](https://a.yandex-team.ru/arcadia/market/infra/java-application/spring-boot-starters/healz-spring-boot-starter/src/main/java/metrics/example).

## Как подключить к проекту не на MJ
Для подключения healz к проектам не на MJ можно воспользоваться [стартером](https://a.yandex-team.ru/arcadia/market/infra/java-application/spring-boot-starters/healz-spring-boot-starter). То есть достаточно добавить в ya.make следующие строчки:
```
PEERDIR(
   market/infra/java-application/spring-boot-starters/healz-spring-boot-starter
)
```