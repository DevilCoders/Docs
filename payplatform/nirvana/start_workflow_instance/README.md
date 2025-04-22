## Утилита для запуска Workflow или Workflow Instance

Запускает Workflow или WorkflowInstance и завершается, не дожидаясь окончания.

### Параметры 

- `--workflow-instance-id=3e9a5af8-8920-44ac-bf51-bdf327866a52` – идентификатор Workflow Instance для запуска. **Обязательный параметр, если не указан Workflow Id**. 
- `--workflow-id=3e9a5af8-8920-44ac-bf51-bdf327866a52` – идентификатор Workflow для запуска. **Обязательный параметр, если не указан Workflow Instance Id**. 
- `--nirvana-server=test.nirvana.yandex-team.ru` – какой сервер Nirvana использовать, продовый или тестовый.
- `--token-filename=./token` – путь к файлу с OAuth токеном для Nirvana.
