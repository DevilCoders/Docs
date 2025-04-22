## Pull до Соломона, Pull до модулей

1. Fetcher забирает данные Агента в pull режиме (шард `(project=my_project; service=pull_modules)`, значение **cluster** выставляется на бэкенде)
2. Агент собирает данные из различных pull модулей

Запуск Агента:
```bash
$ solomon-agent --config ./agent.conf
```

Запуск примера http сервера, из которого Агент может забирать данные:
```bash
$ node simple_http_server.js
```

Проверить наличие данных в Агенте после их сбора из модулей (именно их заберёт Fetcher):
```bash
$ curl -g "http://[::1]:9666/storage/read?project=my_project&service=pull_modules&pretty=true"
```
