# startrek_info - получить информацию о тикете

## Параметры

- `issue` - имя тикета

## Примеры

```yaml
name: example
actions:
  - name: Get status
    startrek_info:
      issue: "{{job_vars.target_ticket}}"
    register: result_info
```

Результат в переменной `result_info`
```json
"result_info": {
	"assignee": null,
	"creator": {
		"id": "azryve"
	},
	"id": "6172858a43afbf12274ec0e6",
	"key": "NOC-19792",
	"status": "inProgress"
}
```

Примеры поля `status`
```
open
needInfo
inProgress
backlog
closed
```