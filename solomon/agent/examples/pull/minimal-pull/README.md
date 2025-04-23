## Минимальная **pull** конфигурация

1. Fetcher забирает данные Агента в pull режиме (шард `(project=my_project; service=my_service)`, значение **cluster** выставляется на бэкенде)
2. Агент получает данные из HTTP запроса (push)

Запуск Агената:
```bash
$ solomon-agent --config ./agent.conf
```

Заливка данных в Агента:
1. *nix:
```bash
$ curl -H "Content-Type: application/json" -d@metrics.json -g "http://[::1]:10050/"
```
2. PowerShell:
```bash
PS> curl -H @{'Content-Type'='application/json'} -InFile metrics.json -Uri "http://[::1]:10050/" -Method 'POST'
```

Проверить наличие данных в Агенте после заливки (именно их заберёт Fetcher):
1. *nix:
```bash
$ curl -g "http://[::1]:9666/storage/read?project=my_project&service=my_service&pretty=true"
```
2. PowerShell:
```bash
PS> curl -Uri "http://[::1]:9666/storage/read?project=my_project&service=my_service&pretty=true"
```
