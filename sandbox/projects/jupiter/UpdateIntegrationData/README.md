# Особенности
Данные sandbox-таски используют внешние зависимости из robot, которые не подтягиваются автоматически. Таким образом, даже если кто-то сломает билд в robot, таски будут продолжать функционировать.

# Я изменил исходный код, как обновить сами таски?
После коммита изменений необходимо запустить две таски **DEPLOY_BINARY_TASK** от нужной ревизии c ```task_type: JUPITER_COMMIT_INTEGRATION_DATA``` в атрибутах и ```target```'ами: 
- ```sandbox/projects/jupiter/UpdateIntegrationData/commit/commit```
- ```sandbox/projects/jupiter/UpdateIntegrationData/create/create```

**Гораздо проще найти предыдущие запуски и склонировать их: тип DEPLOY_BINARY_TASK, owner JUPITER.**
По завершению выполнения обе таски нужно зарелизить.

