## Pull до Соломона, Push до модулей

1. Fetcher забирает данные Агента в pull режиме (шард `(project=my_project; service=push_modules)`, значение **cluster** выставляется на бэкенде)
2. Агент получает данные из HTTP запроса (push)

Запуск Агената:
```bash
$ solomon-agent --config ./agent.conf
```

Заливка данных в Агента:
```bash
$ curl -H "Content-Type: application/json" -d@metrics.json -g "http://[::1]:10050/"
```

Проверить наличие данных в Агенте после заливки (именно их заберёт Fetcher):
```bash
$ curl -g "http://[::1]:9666/storage/read?project=my_project&service=push_modules&pretty=true"
```
