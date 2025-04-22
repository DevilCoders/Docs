Настройка http сервиса, который отдает данные для мониторингов в Голован:
```
host_infra:
    monitoring:
        unistats:
        - workload_id: app_workload
            port: 7032
            path: /unistat
```