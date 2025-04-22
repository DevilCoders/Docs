Конфигурация

```yaml
zookeeper:
  server: "ololo.net.yandex.net,ololo2.net.yandex.net" # список серверов zk
  lock_path: "/grad/server_test2" # путь к lock файлу
  identifier: "myt-grad1.yndx.net" # имя текущего сервера, по умолчанию hostname

internal_metrics_url: "http://olo:22132"  # URL Unified Agent
internal_metrics_sensor: "sensor" # имя сенсора
```
