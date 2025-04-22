## Локальная проверка Docker образа

1.  Должен быть **отключен** `falcon dev`

1.  Должны быть **запущены** вспомогательные сервисы: `falcon start services`

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

Секреты:

```
cat /etc/yandex/taxi-secdist/taxi.json
```

### Логи приложения в облаке

```bash
# stdout
tail -f /var/log/supervisor/lavka-falcon-stdout.log

# stderr
tail -f /var/log/supervisor/lavka-falcon-stderr.log
```
