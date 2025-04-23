Сервис предназначен для периодического выполнения заданий, преимущественно архивации данных.
Сервис является развитием сервиса Scheduler из поставки Infor.

### БД
```sql
use master;
create database Scheduler
use Scheduler;
CREATE LOGIN [scheduler] WITH PASSWORD = 'Passw0rd!';
create user [scheduler] for login [scheduler]
ALTER ROLE db_owner ADD MEMBER [scheduler]
ALTER USER [Scheduler] WITH DEFAULT_SCHEMA = wmwhse1;
use SCPRD
create user [scheduler] for login [scheduler]
ALTER ROLE db_owner ADD MEMBER [scheduler]
ALTER USER [scheduler] WITH DEFAULT_SCHEMA = wmwhse1;
use SCPRDARC
create user [scheduler] for login [scheduler]
ALTER ROLE db_owner ADD MEMBER [scheduler]
```
### Настройки заданий
Задания описываются в ```scheduler2/src/main/resources/quartz_data.xml``` и автоматически добавляются в базу.

### Graceful Shutdown
При завершении работы сервиса всем выполняющимся джобам отправляется сигнал interrupt(). Если джоба реализует InterruptableJob
то будет вызван её метод interrupt и кварц будет ждать пока она завершится. Если не реализует, то будет прибита сразу.

### Настройки мониторинга
История выполнения пишется в Scheduler.dbo.QRTZ_HISTORY

Настройки мониторинга задаются в таблице Scheduler.dbo.job_monitoring_config
* ```runs_number_to_consider``` - сколько последних запусков брать для мониторинга
* Проверяет превышен ли порог между запусками джобы. Если порог превышен, то возвращает ошибку с таймстемпом последнего запуска
  * ```max_delay_time```
  * ```warn_delay_time```
* Проверяет превышен ли порог по длительности работы. Если порог превышен, то возвращает ошибку с максимальным временем работы и таймстемпом начала
  * ```max_execution_time```
  * ```warn_execution_time```

Статус тут GET http://host/scheduler2/health/hangingJobs/archive/canary


* Проверяет превышен ли порог по неуспешным запускам. Если порог превышен, то возвращает ошибки по всем запускам (из числа отслеживаемых)
  * ```max_failed_runs```
  * ```warn_failed_runs```

Статус тут GET http://host/scheduler2/health/failedJobs/{jobGroup}/{jobName}

#### Health Check

GET http://host/scheduler2/scheduler/hc/ping

Делается проверка на живость базы и hangingJobs/archive/canary -
cпециальный джоб, выполняющийся каждую минуту и ничего не делающий

GET http://host/scheduler2/health/failedJobs/archive/canary

### Ручки для управления
#### Список джобов
GET http://host/scheduler2/manage/jobs

fireTime - время следующего запуска

#### Поставить выполнение джоба на паузу/возобновить
POST http://host/scheduler2/manage/job-group/{jobGroup}/jobs/{jobName}/pause

POST http://host/scheduler2/manage/job-group/{jobGroup}/jobs/{jobName}/resume

В списке джобов джоб на паузе имеет state = PAUSED

#### Запустить джоб разово
POST http://host/scheduler2/manage/job-group/{jobGroup}/jobs/{jobName}/execute?p1=v1

Параметры запроса будут переданы в jobDataMap как есть и могут использоваться для управления джобом или переопределения параметров из БД

#### История запусков
GET http://host/scheduler2/manage/job-group/{jobGroup}/jobs/{jobName}/history?limit=10

#### Фикс проблемы с падением джоб по таймауту запросов при использовании TransactionTemplate
Ранее часть транзакций в сервисах выполнялась с использованием бина TransactionTemplate, являющегося синглтоном.
Таким образом, при изменении таймаута запросов через setTimeout() в одном сервисе, происходило его изменение для всех сервисов.
Если таймаут устанавливался меньше, чем необходимо для текущего запроса, выбрасывалось исключение.
Решение: создавать для каждого Дао собственный NamedParameterJdbcTemplate и устанавливать таймаут непосредственно для JdbcTemplate.
