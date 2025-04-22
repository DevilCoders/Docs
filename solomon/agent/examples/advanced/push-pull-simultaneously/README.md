## Работа в обоих режимах (Push, Pull) сразу с созданием новых шардов

В данном примере:
1. Агент получает данные из HTTP запроса (push модуль)
1. Solomon Fetcher забирает из Агента оригинальные (неизменённые) данные (шард `(project=my_project; service=original_service)`, Значение `cluster` выставляется на стороне бэкенда)
1. Агент также отправляет данные в Соломон через PUSH API и перед отправкой разбивает данные на _новые_ шарды (по правилам `ShardKeyOverride`)

Таким образом, в Соломоне появятся данные для шардов:
1. `(project=my_project; service=original_service)`
1. `(project=project1; cluster=cluster1; service=new_service)`
1. `(project=project2; cluster=cluster2; service=new_service)`
1. `(project=project2; cluster=cluster3; service=new_service)`

Запуск Агената:
```bash
$ solomon-agent --config ./agent.conf
```

Заливка данных в Агента:
```bash
$ curl -H "Content-Type: application/json" -d@metrics.json -g "http://[::1]:10050/"
```
