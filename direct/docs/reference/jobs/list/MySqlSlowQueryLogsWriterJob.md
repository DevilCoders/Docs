### Продукт/подсистема

Инфраструтура

### Роль в работе продукта/подсистемы
Получает через api внутреннего Яндекс.Облака slow query логи из кластеров MySQL и записывает их в логброкер.

### Датафлоу
Получает через [cloud-api](https://docs.yandex-team.ru/cloud/managed-mysql/api-ref/grpc/) slow query логи из
[кластеров MySQL](https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/managed-mysql?section=list) и записывает их
в логброкер в топик [direct-mysql-slow-query-log](https://lb.yandex-team.ru/logbroker/accounts/direct/direct-mysql-slow-query-log?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics), откуда они будут переложены [логшаттером](https://wiki.yandex-team.ru/jeri/ppclogshatter) в [кликхаус](https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/managed-clickhouse/cluster/mdbns84iukrpbke13rul/view)
в таблицу `directdb.mysql_slow_query_log`.

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.MySqlSlowQueryLogsWriterJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'slowlogs.MySqlSlowQueryLogsWriterJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [топик в продакшене](https://lb.yandex-team.ru/logbroker/accounts/direct/direct-mysql-slow-query-log?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics)
- таймстемпы последних записанных в логброккер логов можно посмотреть запросом с ppcdev's
  ```shell
  dbs-sql pr:ppcdict "select * from ppc_properties where name like 'mysql_slow_query_logs_writer_%'"
  ```
  поле `timestamp` в `value` не должно отставать по UTC о текущего времени более чем на несколько минут (для кластера ppcdict возможно большее отставание).

### Какая функциональность пострадает от отказа джобы

В логвьювере будет невозможно посмотреть свежие slow query логи с кластеров MySql.

### Как пользователи (или команда) заметят проблему и через какое время

Пользователи не заметят никак, эта ждоба только для внутреннего использования. Команда заметит по отсутствию свежих slow query логов с кластеров MySql в логвьювере.

### Контакты разработчика

Разработчик: [vamenshov](https://staff.yandex-team.ru/vamenshov)

### Желательное время исправления в случае поломки

Желательно починить джобу в течение недели, так как api внутреннего облака отдает логи старше 7-ми дней гораздо медленнее,
чем более новые логи. Поэтому лучше не доводить отставание чтения логов более чем на неделю.

### Способы регулирования работы джобы

#### В конфигурации

В [common-production.conf](https://a.yandex-team.ru/arc_vcs/direct/libs-internal/config/src/main/resources/common-production.conf#L2141):
```yaml
cloud {
  api {
    url: "gw.db.yandex-team.ru", # Адрес api внутреннего Яндекс.Облака
    port: 443
    user_agent: "robot-dir-log-viewer@yandex-team.ru", # юзер-агент для передачи в облако, любая, в принципе, строка
    request_timeout: "180s", #таймаут gRPC клиента (данных передается много, поэтому большой)
  }
}

cloud_iam_default {
  enabled: true # в продакшене должен быт включен
  oauth_token_provider {
    name: "robot-dir-log-viewer" # Имя пользователя, под которым осуществляется чтение слоу логов.
      # Нужно для лучшей читаемости логов самой джобы, никуда не отсылается, в принципе сгодится любая строка
    create_new_iam_token_interval: "1h", # период обновления cloud-iam токена, рекомендуется в доке Яндекс-облака
      # (https://docs.yandex-team.ru/cloud/managed-mysql/api-ref/authentication)
    oauth_token_file: "file:///etc/direct-tokens/yc_robot-dir-log-viewer" #путь к файлу с OAUTH-токеном пользователя,
      # который будет обмениваться на iam-токен Яндекс.Облака. Сейчас используется OAUTH-токен пользователя
      # https://staff.yandex-team.ru/robot-dir-log-viewer. Получить OAUTH-токен для облака можно по ссылке
      # https://oauth.yandex-team.ru/authorize?response_type=token&client_id=8cdb2f6a0dca48398c6880312ee2f78d
  }
}
```

В [app-production.conf](https://a.yandex-team.ru/arc_vcs/direct/jobs/src/main/resources/app-production.conf#L870):

```yaml
cloud_mdb_mysql_slow_query_logs {
  clusters: [ # Имена кластеров, с которых читать mysql slow query логи, секцию можно сгенерировать методом
              # MySqlSlowQueryLogsWriterStatesHelper.getClustersInitialConfig()
		"ppcdict-production",
		"ppcdata1-production",
		......................
		"ppcdata21-production"
	],
  logbroker {
    host: "logbroker.yandex.net" # Хост логброкера
    topic = "direct/direct-mysql-slow-query-log" # Топик логброкера
    tvm_service_name: "logbroker_production" # Имя сервиса из TvmService.java
    timeout: 180s # Таймаут на запись в логброкер
    compression_codec: "lzop" # Кодек для сжатия данных
  },
  job {
    cloud_rows_count_in_batch: 1000 # сколько строк с логами грузить из облака за один запрос.
      # При ошибках о превышении максимальной длины сообщения можно уменьшить до 500
    log_rows_buffer_estimate_size_in_megabytes: 16   # Сколько примерно мегабайт неотправленных записей с логами
      # поддерживать на лету. Если из облака загружено, но пока не отправлено строк с логами на больший объем,
      # чем указанное в этом параметре значение, то новые строки не будут подгружаться из облака, пока объем
      # оставшихся логов не станет меньше значения этого параметра
    exclude_queries_filter: " sleep(" # Запросы содержащие эту строку не будут загружены в логброкер
    new_cluster_logs_start_days_ago: 7 # На сколько дней назад начинать читать слоу логи для новых кластеров
    direct_infra_cloud_folder_id: "fooa07bcrr7souccreru" # Идентификатор облака Директа. Нужен для получения
      # информации о кластерах mySQL
    enable_slow_log_record_raw_text_field: true # Добавлять к распарсеным записям slow query лога
      # поле с исходной строкой, полученной из cloud api, или не добавлять. Это поле весит примерно
      # как все остальные поля вместе взятые, то есть включение этого поля удваивает объем данных.
      # Однако пока джоба не устоялась, имеет смысл добавлять это поле для целей отладки
  }
}
```
#### В ppc пропертях

Для каждого MySql кластера джоба создает проперти вида `mysql_slow_query_logs_writer_$CLUSTER_NAME_cluster_state`.
В них хранится идентификатор кластера, временная метка последней прочитанной записи slow query лога, и флаг доступности кластера.
Пример проперти:

```json
{
    "clusterId":"mdb2g4pi3mstnn950lod", // идентификатор кластера
    "version":1, // Версия проперти, при изменении руками увеличить на 1
    "timestamp":"2021-12-09T12:40:40Z", // Таймстемп последней отправленной в логброкер записи slow query лога
    "positionInTimestamp":1, // Позиция последней отправленной в логброкер записи slow query лога внутри таймстемпа
    "available":true // флаг доступности кластера (только читается)
}
```

Если проперти для кластера есть, а в `app-production.conf` приложения `jobs` в секции `cloud_mdb_mysql_slow_query_logs.clusters`
кластера нет, джоба не будет читать логи для этого кластера.

Если проперти для кластера нет, а в`app-production.conf` приложения `jobs` в секции `cloud_mdb_mysql_slow_query_logs.clusters`
кластер задан, то джоба сходит в api внутреннего Яндекс.Облака, получит идентификатор кластера, создаст новую проперти
`mysql_slow_query_logs_writer_$CLUSTER_NAME_cluster_state` с таймстемпом последней отправленной в логброкер записи
&laquo;текущее время минус 7 дней&raquo; (7 - значение параметра `cloud_mdb_mysql_slow_query_logs.job.new_cluster_logs_start_days_ago`), и начнет читать логи с этой метки.

Если и в конфиге кластер есть, и проперти есть, но в проперти выставить `"available":false`, то джоба перестанет
грузить данные с этого кластера. Причем после изменения проперти в базе перезапускать джобу или приложение `jobs`
не нужно, она подхватит новое значение на лету. 

Остановить загрузку данных для кластера с именем `$CLUSTER_NAME` можно командой:
```shell
CLUSTER_NAME=ИМЯ_КЛАСТЕРА // например, ppcdata13-production
dbs-sql pr:ppcdict "update ppc_properties set value=replace(value, ':true', ':false') where name='mysql_slow_query_logs_writer_${CLUSTER_NAME}_cluster_state'";
dbs-sql pr:ppcdict "select name, value from ppc_properties where name='mysql_slow_query_logs_writer_${CLUSTER_NAME}_cluster_state'";
```

Возобновить загрузку данных для кластера с именем `$CLUSTER_NAME` можно командой:
```shell
CLUSTER_NAME=ИМЯ_КЛАСТЕРА // например, ppcdata13-production
dbs-sql pr:ppcdict "update ppc_properties set value=replace(value, ':false', ':true') where name='mysql_slow_query_logs_writer_${CLUSTER_NAME}_cluster_state'";
dbs-sql pr:ppcdict "select name, value from ppc_properties where name='mysql_slow_query_logs_writer_${CLUSTER_NAME}_cluster_state'";
```

Таймстемпы последних записанных в логброккер логов можно посмотреть запросом с ppcdev's
```shell
dbs-sql pr:ppcdict "select * from ppc_properties where name like 'mysql_slow_query_logs_writer_%'"
 ```

Удалить проперти для всех кластеров можно запросом с ppcdev's
```shell
dbs-sql pr:ppcdict "delete from ppc_properties where name like 'mysql_slow_query_logs_writer_%'"
 ```
Джоба создаст после этого новые проперти для всех кластеров из конфига, и начнет читать с них логи заново.

То же самое можно сделать и для конкретного кластера с именем `$CLUSTER_NAME`. Просмотреть запросом
```shell
CLUSTER_NAME=ИМЯ_КЛАСТЕРА // например, ppcdata13-production
dbs-sql pr:ppcdict "select * from ppc_properties where name like 'mysql_slow_query_logs_writer_${CLUSTER_NAME}_cluster_state'"
 ```
и удалить проперти запросом
```shell
CLUSTER_NAME=ИМЯ_КЛАСТЕРА // например, ppcdata13-production
dbs-sql pr:ppcdict "delete from ppc_properties where name like 'mysql_slow_query_logs_writer_${CLUSTER_NAME}_cluster_state'"
 ```

### Дополнительно: тонкости и подводные камни
Если удалить проперти для кластера, джоба начнет читать с него логи начиная с текущей даты минус
`cloud_mdb_mysql_slow_query_logs.job.new_cluster_logs_start_days_ago` дней. В этом случае скорее всего некоторые логи
будут повторно записаны в логброкер, а потом логшаттером в кликхаус. В кликхаусе дедупликация происходит в фоновом режиме,
поэтому в логвьювере в логе `mysql_slow_query_log` какое-то время будут присутствовать дубликаты.
