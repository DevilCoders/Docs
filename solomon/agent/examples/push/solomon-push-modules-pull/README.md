## Push до Соломона, Pull до модулей

1. Агент отправляет данные в Соломон в push режиме (шард `(project=my_project; cluster=my_cluster; service=pull_modules)`)
2. Агент собирает данные из Python модуля (в pull режиме)

Запуск Агента:
```bash
$ solomon-agent --config ./agent.conf
```
