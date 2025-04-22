Directory with config files for logkeeper-minion.


Example config:
```yaml
config:
  # abc сервис для подсчета потребления
  ABC: 'report'
  # по этой директиве формируется путь до лога в хранилище
  DST_DIR: 'snippet-tms'
  # путь до логов на инстансе, logs/<APP>
  APP: 'snippet-tms'
  # regexp для логов
  PATTERN: 'snippet-tms.log.*.gz'
  # список сервисов, с которых забирать логи
  SERVICE_NAME:
      - 'testing_market_snippet_tms_sas'
      - 'testing_market_snippet_tms_vla'
  # Срок жизни лога в днях
  LIFETIME: 91
  # Удалять ли файл с инстанса после его забора
  KEEP_FILE: True
```
