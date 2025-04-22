# Восстановление Nanny-сервисов из бэкапа

## Краткое описание настроек бэкапа {intro}

* бэкап реализован через [scli](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/service_repo_client/bin). Подробнее здесь [SWAT-4453](https://st.yandex-team.ru/SWAT-4453)
* запуск `scli` осуществляет шедуллер [BACKUP_NANNY_SERVICES](https://sandbox.yandex-team.ru/scheduler/10717/view)
* бэкап сохраняется как tar.gz-ресурс: [BACKUP_NANNY_ARCHIVE](https://sandbox.yandex-team.ru/resources/?type=BACKUP_NANNY_ARCHIVE&page=1&pageCapacity=20)

## Восстановление сервисов {#restore}

### Scli {#scli}

Для восстановления необходим клиент `scli`. Собираем из [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/service_repo_client), либо качаем бинарь для x86_64:

```bash
curl -vOJ 'http://proxy.sandbox.yandex-team.ru/last/NANNY_SCLI_BIN'
```

## Инструкция по восстановлению {#restore-steps}

```bash
curl -vOJ 'http://proxy.sandbox.yandex-team.ru/last/BACKUP_NANNY_ARCHIVE' # качаем последний бэкап из сэндбокса
tar -xvzf nanny_backup.tar.gz
./scli -d nanny_backup restore <service_id> -t <NANNY_OAUTH_TOKEN>
```
