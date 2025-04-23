## Утилита для изменения глобальных параметров Workflow Instance

Перезаписывает глобальные параметры Workflow Instance на основе переданных.
Если какого-то из параметров Workflow Instance не будет во входных данных, то он сохранит прежнее значение.

### Параметры 

- `--workflow-instance-id=3e9a5af8-8920-44ac-bf51-bdf327866a52` – идентификатор Workflow Instance, глобальные параметры которого нужно изменить.
- `--nirvana-server=test.nirvana.yandex-team.ru` – какой сервер Nirvana использовать, продовый или тестовый.
- `--token-filename=./token` – путь к файлу с OAuth токеном для Nirvana.
- `--parameters-filename` – путь к файлу, содержащему описания значений параметров. Формат:
```json
{
     "workflow_id": "825d0224-5037-40c5-86dc-8055425fdca5",
     "environment": "hahn"  
}
```
