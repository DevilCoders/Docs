## Использование доп. тредпулов, указание логирования и размера хранилища

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

В этой конфигурации стоит обратить внимание на использование в конфиге:
1. **Io** тредупла
2. секции **Storage**
3. секции **Logger**

[Подробнее](https://wiki.yandex-team.ru/solomon/agent/how-to-run/#konfigagenta)
