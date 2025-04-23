## Локальная проверка Docker образа

1.  Должен быть **отключен** `pigeon dev`

1.  Должны быть **запущены** вспомогательные сервисы: `pigeon start services`

1.  ```bash
    bash dockers/rtc/test-image-locally.sh
    ```

## Локальная проверка обработки taxi.json

```bash
bash dockers/rtc/test-secrets-locally.sh
```

## Quick tips

### Папка приложения в облаке

```bash
ls -la /usr/local/app
```

### Закрыть http трафик на инстансе

```bash
iptruler 80 down syn

# включить обратно
iptruler 80 up syn

# открыть всё очистив ранее внесённые записи
iptruler flush all
```

### Логи приложения в облаке

```bash
# syslog
tail -f /var/log/yandex/taxi-lavka-pigeon/taxi.log

# stdout
tail -f /var/log/supervisor/lavka-pigeon-stdout.log

# stderr
tail -f /var/log/supervisor/lavka-pigeon-stderr.log
```
