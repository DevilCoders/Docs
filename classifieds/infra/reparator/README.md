# Info

## as service

<http://localhost:31336/api/start_repair> - GET запуск починки (repair)

<http://localhost:31336/api/start_compaction> - GET запуск сжатия (compaction)

<http://localhost:31336/api/status> - GET состояние починки

<http://localhost:31336/metrics> - prometheus metrics

## as cli

```sh
~ reparator -compact
~ reparator -repair
```
