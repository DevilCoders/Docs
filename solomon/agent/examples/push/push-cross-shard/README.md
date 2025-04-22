## Push с разбиением данных на новые шарды

1. Агент отправляет данные в Соломон в push режиме (из данных одного шарда в несколько _новых_ шардов!)
2. Агент получает данные из HTTP запроса (push)
3. Перед отправкой данных Агент разбивает их на несколько шардов, по [правилам(ShardKeyOverride)](https://wiki.yandex-team.ru/solomon/agent/how-to-run/#konfigagenta), указанным в конфиге

Запуск Агента:
```bash
$ solomon-agent --config ./agent.conf
```

Заливка данных в Агента:
```bash
$ curl -H "Content-Type: application/json" -d@metrics.json -g "http://[::1]:10050/"
```
