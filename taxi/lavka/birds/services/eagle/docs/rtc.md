## Локальная проверка Docker образа

1.  Должен быть **отключен** `eagle dev`

1.  Должны быть **запущены** вспомогательные сервисы: `eagle start services`

1.  ```bash
    bash services/eagle/dockers/rtc/test-image-locally.sh
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

### Логи приложения в облаке

```bash
# syslog
tail -f /var/log/yandex/taxi-lavka-eagle/taxi.log

# stdout
tail -f /var/log/supervisor/lavka-eagle-stdout.log

# stderr
tail -f /var/log/supervisor/lavka-eagle-stderr.log
```
