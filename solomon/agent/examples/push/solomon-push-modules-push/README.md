## Push до Соломона, Push до модулей

1. Агент отправляет данные в Соломон в push режиме (шард `(project=my_project; cluster=my_cluster; service=push_modules)`)
2. Агент получает данные из HTTP запроса (push)

Запуск Агената:
```bash
$ solomon-agent --config ./agent.conf
```

Заливка данных в Агента:
```bash
$ curl -H "Content-Type: application/json" -d@metrics.json -g "http://[::1]:10050/"
```
