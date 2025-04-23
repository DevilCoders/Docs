## Push с авторизацией

1. Агент отправляет данные в Соломон в push режиме (шард `(project=my_project; cluster=my_cluster; service=test_auth)`)
2. Агент собирает данные из Python модуля (в pull режиме)
3. Агент сам генерирует IAM и TVM токены авторизации. [Подробнее](https://wiki.yandex-team.ru/solomon/agent/how-to-run/#auth)

Запуск Агента:
```bash
solomon-agent --config ./agent.conf
```
