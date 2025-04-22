# Tms-http

### Описание 

Библиотека для http-ручек к tms-core-quartz2 

Предоставляет два get метода: 

1. /health/hangingJobs - метод возвращает строку в формате мониторинга (1/3;Message). 
Проверяет есть ли среди запущенных джоб такие, что выполняются дольше установленного порога,
и, есть ли среди последних запусков джоб, которые сейчас не выполняются, такие,
что выполнялись дольше установленного порога.  
2. /health/failedJobs - метод возвращает строку в формате мониторинга (1/3;Message).
 Проверяет есть ли среди всех джоб зарегистрированных в TMS такие у которых среди последних запусков было
 больше неуспешных выполнений, чем значение заданного порога.
 
 
### 1. Как работает

Библиотека использует специальную таблицу (по умолчанию job_monitoring_config),
в которой задаются пороговые значения выполнения джоб: 
1. max_delay_time (warn_delay_time) - максимальное время задержки(время для ворнинга): время,
 которое джоба может не запускаться; Если джоба новая, то время будет остчитываться от tracking_start_time.
2. max_execution_time (warn_execution_time) - максмальное время(время для ворнинга), которое джоба может исполняться;
3. max_failed_runs (warn_failed_runs) - количество неуспешных запусков(количество для ворнинга), о котором нужно нотифицировать;
4. runs_number_to_consider - общее количество запусков, которое нужно проанализировать.

Свойства из пунктов 3. и 4. связаны: берем runs_number_to_consider последних логов выполнения джобы,
 считаем количество не OK, сравниваем это количество с max_failed_runs.
 
### 2. Как подключить

Для подключения необходимо:
1. добавить зависимость на библиотеку: 
`    compile("ru.yandex.market.delivery.commons:tms-http:1.0.0")
`
2. импортировать бин конфигурации TmsPluginConfiguration.class
3. написать миграцию, которая создаст и заполнит нужными значениями таблицу 
job_monitoring_config. Название этой таблицы можно задать пропертей `tms.monitoring.config.table`.
4. * В текущей версии стоит добавить бин CacheManeger в контекст спринг-приложения.

```java
@Bean
public CacheManager cacheManager() {
    return new ConcurrentMapCacheManager();
}```

Стоит учитывать, что библиотека надеется на наличие JdbcTemplate-а с настроенным dataSource-ом и просто его автовайрит.

Шаблон скрипта: 

```sql
create table job_monitoring_config
 (  
 	job_name VARCHAR(256) NOT NULL 
 		CONSTRAINT job_monitoring_config_pkey
 			PRIMARY KEY,
 	max_delay_time INTEGER NOT NULL,
 	warn_delay_time INTEGER NOT NULL,
 	max_execution_time INTEGER NOT NULL,
 	warn_execution_time INTEGER NOT NULL,
 	max_failed_runs INTEGER NOT NULL,
 	warn_failed_runs INTEGER NOT NULL,
 	runs_number_to_consider INTEGER NOT NULL,
    tracking_start_time     TIMESTAMP    NOT NULL DEFAULT current_timestamp
 );

 COMMENT ON COLUMN job_monitoring_config.job_name IS 'Имя tms-задачи';
 COMMENT ON COLUMN job_monitoring_config.max_delay_time
  IS 'Максимальное время между завершением джобы и следующем её запуском';
 COMMENT ON COLUMN job_monitoring_config.warn_delay_time
  IS 'Время для ворнинга между завершением джобы и следующем её запуском';
 COMMENT ON COLUMN job_monitoring_config.max_execution_time IS 'Максимальное время выполнения';
COMMENT ON COLUMN job_monitoring_config.warn_execution_time IS 'Время выполнения для ворнинга';
 COMMENT ON COLUMN job_monitoring_config.max_failed_runs IS 'Критичное количество неуспешных запусков';
COMMENT ON COLUMN job_monitoring_config.warn_failed_runs IS 'Количество неуспешных запусков для ворнинга';
 COMMENT ON COLUMN job_monitoring_config.runs_number_to_consider
  IS 'Количество последних запусков, которое проверяем на предмет неуспешных выполнений';
 COMMENT ON COLUMN job_monitoring_config.tracking_start_time 
 IS 'Время, с которого нужно считать незапущенные ни разу джобы задерживающимися'
```


Если по какой-то причине not null не будут проставлены и значений max_delay_time или max_execution_time не будет,
 то будет осуществлена попытка взять эти значения из пропертей:
 `tms.default.max.delay.time` по умолчанию: 1200 с.
 `tms.default.max.execution.time` по умолчанию: 1800 с. 
 
Также есть пропертя `tms.http.configs.cache.lifespan` в минутах контролирует время жизни кэша конфигов,
 по умолчанию: 5 минут, если поставить 0, то конфиги кэшироваться не будут.
 
Для контроля того, на сколько кэшируется результат OK можно через пропертю `tms.http.ok.cache.lifespan` в миллисекундах,
 которая по дефолту выставляется в 60000 (1 минута) 

